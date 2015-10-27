---
layout: post
title:  "Restarting network on ubuntu server"
date:   2015-04-06 08:29:11
categories: ubuntu linux network
---
U can use command:
`ifconfig eth0 down && ifconfig eth0 up`
where `eth0` - your network interface is called
or U can use:
`sudo ifdown --exclude=lo -a && sudo ifup --exclude=lo -a`
