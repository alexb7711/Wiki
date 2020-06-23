---
title: How To Easily Access your Home Network From Anywhere With Dynamic DNS
header-includes:
	- \usepackage[a4paper, margin=0.5in]{geometry}
	- \fontfamily{qag} 
	- \renewcommand{\familydefault}{\sfdefault}
---

# What is Dynamic DNS
DNS (Domain Name System) is the protocal that converts a domain name into an IP address. So rather than connecting to your home network by IP address, why not use a DDNS (Dynamic DNS)? The reason that we would want to use DDNS rather than just a DNS is because home networks are treated differently. The ISP has a big pool of addresses, and they share them with everyone on an as-needed basis.

# What You Need
There are two different methods you can use to keep your DDNS address up to date:

## A DDNS Host
First and foremost, you need a DDNS host. If you want a free DDNS provider you can look at: [No-IP](https://www.noip.com/),  [Dynu Systems](http://www.dynu.com/),  [Zonomi DNS Hosting](https://zonomi.com/) just to name a few.

## A Router with DDNS Support
When your router supports DDNS services, you can simply plugin your DDNS provider information and your router will automatically update the address behind the scenes.

## A Local Update Client
If your router does not support DDNS services, you will need a local client to run on a frequently used computer somewhere on your home network.

# References
[How To Geek](https://www.howtogeek.com/66438/how-to-easily-access-your-home-network-from-anywhere-with-ddns/)
