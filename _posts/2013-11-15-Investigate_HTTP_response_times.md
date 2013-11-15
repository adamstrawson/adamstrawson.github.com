---
layout: post
title: "Investigate HTTP response times"
---

I was investigating some odd behaviour on [Smokeping](http://oss.oetiker.ch/smokeping/) and I wanted a quick way of finding HTTP response times for each step of the route.

I put together this bash script that does a Curl on a given Host/IP and returns the time to connect, the transfer start time, and the total response time.

<script src="https://gist.github.com/adamstrawson/7488317.js"></script>

Please feel free to use, improvement suggestions are welcome.
