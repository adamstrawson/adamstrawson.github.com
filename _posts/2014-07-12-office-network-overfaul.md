---
layout: post
title: "Office Network Overhaul"
---
At <a href="http://tsrmatters.co.uk" target="_blank">TSR Towers</a>, we recently undertook an infrastructure overhaul of the network that runs our office as we had outgrown our existing setup.

The project was a team effort, consisting of <a href="http://www.mason-it.co.uk/" target="_blank">Mark & Chris from Mason IT</a>, <a href="http://www.supporttime.com/" target="_blank">Rob from Support Time</a>, Pete our CTO and myself.

### Why Upgrade

Not only were we hitting performance bottlenecks with our existing setup, our WiFi was unstable, and wasn't able to handle the amount of wireless devices in the office (~100), we had also reached capacity and all 96 available ports were in use. We could have added another switch to the chain, but it wouldn't solve our other issues.  
Also since the switches were daisy chained together, it wasn't too reliable, if we happened to have lost one switch (We never did may I add) we would then lose all networking below that chain. 

### Previous Setup

Our previous network consisted of the following:

* 4x Cisco SG300-28 Gigabit POE Managed Switches
* 1x Cisco 1941 Router
* 1x Cisco ASA 5505
* 4x Cisco AP541N Dual Band Wireless AP's 

All the Ethernet cabling was Cat5e.

In terms of network topology, everything was pretty standard. All devices ran of the same VLAN, so this was another reason to upgrade as we were getting close to maxing out the subnet.

The rack looked like this:

![Rack Before](http://08b00f2c4f064c98329c-57bbaadb49146f0ad4c2f3b5b1587005.r9.cf3.rackcdn.com/pre-rack.jpg =350x)

### New Setup

So, knowing what we needed to resolve, we decided to go with the following hardware:

* 1x Huawei Quidway S7706 for our backbone
* 2x 48 Port Gigabit POE blades for the Quidway
* 1x Cisco ASA 5515
* 2x Cisco 1941 Routers
* 1x Huawei AC6005 AP Controller
* 5x Huawei AP6010 WLAN Access Points

The Huawei Quidway is powerful enough to power our entire building, let alone our floor! It has capacity for 240 x 10 Gigabit POE ports, Maximum switching capacity to 5.12 Tbps. It also has improved reliability with fault detection, cooling and redundant power supplies. 

We've introduced a second Cisco 1941 router, one for each of our two ISP lines, set up with BGP failover should one ISP go down. We've also upgraded our ASA, running Cisco Prime Security Manager. 

Our WLAN has improved drastically too, we've improved the coverage throughout the office, and introduced a central controller. 

All the cabling has been replaced with colour coded CAT6 (Red for core/backbone, Yellow for Internal (Printers, etc), Green for general use (PCs, etc)).

We've also introduced multiple vlans (PC's, Wireless, Servers, etc) and Wireless Networks (Guest, Staff, All-Access, plus an additional hidden network for our QA team which uses a standard DSL connection so they can test outside of our fibre line).

### The Upgrade

The upgrade was going to take a few days to complete, so we had to plan it with zero downtime for the office staff. 

On the Sunday, Rob, Pete, and Myself shut everything down, and moved all the exiting Cisco Switches to our rack that houses the internal servers, to make room for the Quidway going in the following day. We installed the additional router, and cleaned up all the existing cabling and changed how the power was distributed across the rack.

This is how it looked during and after this:

![Rack Mid Empty](http://08b00f2c4f064c98329c-57bbaadb49146f0ad4c2f3b5b1587005.r9.cf3.rackcdn.com/mid-rack1.jpg =350x)
![Rack Mid Moved](http://08b00f2c4f064c98329c-57bbaadb49146f0ad4c2f3b5b1587005.r9.cf3.rackcdn.com/mid-rack2.jpg =350x)

Mason IT arrived on the monday to do most of the grunt work, installing and configuring the new hardware, this lasted two days, and all with about 30mins downtime while everything was switched over to the new network. (The office didn't mind since there was a bake-off going on at the time!)

After all this, it resulted in our rack looking like this:

![Rack Mid Moved](http://08b00f2c4f064c98329c-57bbaadb49146f0ad4c2f3b5b1587005.r9.cf3.rackcdn.com/post-rack1.jpg =350x)
![Rack Mid Moved](http://08b00f2c4f064c98329c-57bbaadb49146f0ad4c2f3b5b1587005.r9.cf3.rackcdn.com/post-rack2.jpg =350x)

I'd have preferred to have had a network cabinet so that we had room for vertical cable trays down the sides, but we had to make do with the existing rack, so cables aren't as neat as I would have wanted, but nonetheless, happy with the results.

Funnily enough, a few after installing this we've already outgrown it and have had to order an additional 48 Gigabit blade!

