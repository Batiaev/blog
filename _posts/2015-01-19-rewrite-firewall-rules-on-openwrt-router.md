---
layout: post
title:  "Rewrite firewall rules on OpenWrt Roouter"
date:   2015-01-19 23:25:11
categories: linux operwrt firewall router
---

- Connect to router
 `ssh -p 2222 root@router`
- Open firewall config
 `nano /etc/firewall.user`
- Add folloving lines
	WAN='eth0'
	iptables -A input_rule -i $WAN -p tcp --dport 2223 -j ACCEPT
- Restart firewall
 `/etc/init.d/firewall restart`