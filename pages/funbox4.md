---
layout: page
title: Funbox CTF - Medium
permalink: /funbox4/
---
![Funbox CTF](https://www.vulnhub.com/entry/funbox-ctf,546/)<br>

Funbox CTF comes from a series of 11 boxes. 

Goal: use priviledge escalation to gain root access to the target machine.
Hint: Case sensitive with using Nikto and need a minimum of 15 mins to find the user.
<hr>
Target Mac address: 08:00:27:4f:b1:d6
<hr>

1. Netdiscover

We know our Target machine's Mac address. We need to do a netdiscover to find the IP address to the machine. 

![step1]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_1.png)

2. Nmap

Now that we have identified our target IP we should run an nmap scan to see what information we can find on the target network. 

![step2]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_2.png)
4. 

