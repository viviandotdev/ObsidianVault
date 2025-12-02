---
created: 2024-05-16 17:33
modified: 2025-06-28T08:05:32-04:00
---
up::  [[How to deploy an api using Digital Ocean and Dokku]]
type:: #note/how-to
tags:: [[dns]]

**Do this first to make sure it propagates**

1. Purchase a domain at
	- [Go Daddy](https://dcc.godaddy.com/control/dnsmanagement?domainName=retwitter.site&subtab=nameservers)
	- [Namecheap](https://www.namecheap.com/)
	- [Porkbun](https://porkbun.com/)
2. Add DNS records
	(host: api (name of your app)
	(value: is the IP address of your droplet)
	![[Screenshot 2024-05-16 at 2.59.54 PM.png]]
![[Screenshot 2024-05-18 at 2.25.20 PM.png]]

**Check if DNS has propagated**
[DNS Propagation Checker - Global DNS Testing Tool](https://www.whatsmydns.net/#A/lireddit-api.rereddit.site)
