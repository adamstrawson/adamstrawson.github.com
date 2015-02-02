---
layout: post
title: "Why you should use experimental projects"
---

Awhile back we spec'd out a project that needed a number of MySQL servers, each with a different database, replicating to a single instance for data aggregation and reporting use. 

We discovered [Multi-source Replication](http://mysqlhighavailability.com/5-7-5-labs-multi-source-replication/). Annoyingly this was only available in MySQL 5.7 Development Release. There was mentions of it in MariaDB, but it wasn't production ready either.

After much discussion, the benefits of the end product out weighed the cons of it not being a 'production ready' release. Plus it was only for internal use which lowered the risks. A proof of concept was thrown together, everything worked as expected, so out into our 'production' it went.

Everything worked fine for around a month, it was stable, was meeting our needs and was coping with the traffic from three large replication channels.

Then came the errors.. Replication started to fail randomly, and for odd reasons too. I won't go into detail about the errors, but they left us scratching our heads for hours!

Long story short, MariaDB's Multi-source replication was now production ready, and so the decision was made to migrate to MariaDB. (We're still early days into this, so who knows if this will pay off).

So, we realised we made a mistake using an experimental project for a 'production' service.. but actually on reflection I don't think we did..

Yes we wasted a lot of man hours going down the MySQL 5.7 route, and more so trying to resolve issues with it, but really I'd say I've learnt from it, more than I ever did when using a stable MySQL version. 

My reasons behind this is that it threw errors that a stable version might not have, a stable version tends to just work out the box, it might throw the odd error every now and then, but it's usually a common error that's really easy to resolve. But the kind of errors that this experimental version were giving us were errors that I haven't experienced before, it meant that I had to do more research, it wasn't something you would find on StackOverflow, or with a quick Google!

I loved this, it was a new challenge, troubleshooting something that not many people had experienced. It meant that I had to dig deeper then I ever had into the MySQL docs, learning things I would never have learnt before. 

I'm not saying you should all go off and run experimental projects in production just so you can give yourself a challenge (That's my disclaimer!) But I'd recommend getting involved in development releases. If it doesn't break then great, but when it does, give yourself the challenge and try and resolve it, it's good fun and you'll be surprised by what you learn!

Learnings a big part of our industry, push yourself and try something experimental.
