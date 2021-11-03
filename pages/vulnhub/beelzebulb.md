---
layout: page
title: Beelzebulb 1 - Easy
permalink: /beelzebulb/
---
[Click here to download Beelzebulb 1](https://www.vulnhub.com/entry/beelzebub-1,742/)<br>

Goal: use priviledge escalation to gain root access to the target machine.

<hr>
Target Mac address: 08:00:27:ad:b0:ab
<hr>

![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_1.png)

1. **Netdiscover**<br><br>
     We have the target machines mac address from setting up the target machine. We can use netdiscover to see if we can find the IP address by matching it with the results. 

    ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_2.png)
