---
layout: post
title: "Redis-Flex: An ActionScript Library to integrate with Redis"
date: 2011-06-13 20:40
comments: true
categories: flex
---
Announcing <a href="https://github.com/danielwanja/redis_flex">redis flex</a>  An ActionScript Library to integrate with Redis.

A while back I looked into accessing Redis directly from Flex and I found an existing library, <a href="https://github.com/claus/as3redis">as3redis</a> that however didn't support the new unified request protocol.  So I wrote a minimalist wrapper that now allows to send commands to a redis server.

To access the Redis server from Flex just instantiate a Redis instance:

<!--more-->

``` xml
    <redis:Redis id="server"
                 connected="server_connectedHandler(event)"
                 result="server_resultHandler(event)" />
```

Then you can send commands:

``` javascript
    server.send("SET A 123");
    server.send("GET A");
    server.send(["rpush", "messages", "message one"]);
```


Note it's not a good idea to connect a Flex application directly to Redis. Redis is usually used in the context of an application server that protects it's access in the same way that Flex doesn't connect directly to a database. However they may be cases that this could be useful.

Enjoy!

Daniel


