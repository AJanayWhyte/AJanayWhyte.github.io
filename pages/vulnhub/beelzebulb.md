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
     I have the target machines mac address from setting up the target machine. I can use netdiscover to see if I can find the IP address by matching it with the results. 

    ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_2.png)
    
1. **Nmap**<br><br>

     Now that I have found the IP address for the target machine. We should scan to see what we can find on the target network. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_3.png)
     
     As we can see here there are two ports open on the target network. Port 22 - ssh, and port 80 - http. We should verify whether or not there is an active url.
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_4.png)
     
1. **Gobuster**

     I decided to use gobuster to see what directories I could find attached to the IP address for the target network. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_5.png)
