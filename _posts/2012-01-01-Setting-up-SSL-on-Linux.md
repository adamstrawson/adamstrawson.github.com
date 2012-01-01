                             ---
layout: post
title: "Setting up SSL on a Linux server"
---

I'm writing this guide for my future reference, but if others find it useful then that's a bonus!

First of all, my set-up is as follows:

1. OS: Linux, Ubuntu 10.04.3 LTS
2. Provider: RackSpace Cloud
3. Standard LAMP configuration
4. [Byobu](https://launchpad.net/byobu), just for bouncing around in Terminal   

You'll need to sign up for an SSL certificate, For basic, nothing fancy SSL's I recommend [Namecheap Comodo SSL](http://www.namecheap.com/ssl-certificates/comodo.aspx?aff=26395)

Now, you'll need to make sure you have the following packages installed on your server.

`<code>` 
	apt-get install openssl;
	a2enmod ssl;
`</code>`   

If you've signed up with [Namecheap](http://www.namecheap.com/ssl-certificates/comodo.aspx?aff=26395), once you've purchased your SSL the will ask you for a CSR

Run the following and create a RSA private key for your server. 
   
`<code>`  
	openssl req -nodes -newkey rsa:2048 -keyout YOURDOMAIN.key -out YOURDOMAIN.csr      
`</code>`          

When you run the above, it'll ask you a few questions (Replace my answers with yours):
     
`<code>`   
	Country Name (2 letter code) [AU]: GB
	State or Province Name (full name) [Some-State]: Haywards Heath
	Locality Name (eg, city) []: West Sussex
	Organization Name (eg, company) [Internet Widgits Pty Ltd]: MyCompany Ltd
	Organizational Unit Name (eg, section) []: IT
	Common Name (eg, YOUR name) []: mysubdomain.mydomain.com
	Email Address []:             
`</code>` 

Enter the following 'extra' attributes to be sent with your certificate request
         
`<code>` 
	A challenge password []: 
	An optional company name []:
`</code>`

Once you're done, open the generated YOURDOMAIN.csr file and copy its contents into the text box on Namecheap. 

Follow the Namecheap steps to finish your order.

Once you've completed the order you will received an email containing a ZIP file. Extract the content and upload it to your server at /etc/ssl/

After you have uploaded the files, create a new site-available in apache2 sites-available, do the following in the sites available directory:

`<code>`   
	cd /etc/apache2/sites-available;
	cp default-ssl YOURDOMAIN-ssl
`</code>` 

Edit the domain.com-ssl to match the directory and alias settings of your current non-ssl domain, and make sure the following lines are filled out properly with the correct paths within the config.

`<code>`   
	SSLCertificateFile /etc/ssl/YOURDOMAIN.crt
	SSLCertificateKeyFile /etc/ssl/YOURDOMAIN.key
	SSLCACertificateFile /etc/ssl/PositiveSSLCA.crt
`</code>`                         

Lastly, enable the new domain-ssl configuration in apache, reload apache and restart.

`<code>`   
	a2ensite YOURDOMAIN-ssl;
	/etc/init.d/apache2 reload;
`</code>`

Then we're done, Congrats!     

