---
layout: post
title: "Log Format"
---

I came across a brilliant example of formatting logs, and posting it here not only for my future reference, but hopefully useful for others too.

The log format has a few specific goals:

- Be human readable.  
- Be machine parsable.  
- Be easy for sleepy ops folks to figure out why things are pear-shaped at 3:30AM using standard UNIXy tools like tail and grep.

The logging output looks like this:

    TRACE [2010-04-06 06:42:35,271] com.example.dw.Thing: Contemplating doing a thing.  
    DEBUG [2010-04-06 06:42:35,274] com.example.dw.Thing: About to do a thing.  
    INFO  [2010-04-06 06:42:35,274] com.example.dw.Thing: Doing a thing  
    WARN  [2010-04-06 06:42:35,275] com.example.dw.Thing: Doing a thing  
    ERROR [2010-04-06 06:42:35,275] com.example.dw.Thing: This may get ugly.  
    ! java.lang.RuntimeException: oh noes!  
    ! at com.example.dw.Thing.run(Thing.java:16)  
    !

A few items of note:

All timestamps are in UTC and ISO 8601 format.

You can grep for messages of a specific level really easily:  
    tail -f dw.log | grep '^WARN'

You can grep for messages from a specific class or package really easily:  
    tail -f dw.log | grep 'com.example.dw.Thing'

You can even pull out full exception stack traces, plus the accompanying log message:  
    tail -f dw.log | grep -B 1 '^\!'

Original Source: [http://dropwizard.codahale.com/manual/core/#logging](http://dropwizard.codahale.com/manual/core/#logging)
