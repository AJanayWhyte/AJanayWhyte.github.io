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

     Now that I have found the IP address for the target machine. I should scan to see what I can find on the target network. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_3.png){:height="75%" width="75%"}
     
     I can see here there are two ports open on the target network. Port 22 - ssh, and port 80 - http. I should verify whether or not there is an active url.
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_4.png)
     
1. **Gobuster**<br><br>

     I decided to use gobuster to see what directories I could find attached to the IP address for the target network. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_5.png)
     
     It seems that there is a directory called phpmyadmin. When I added the directory extension to the end of my url it opened up to a login page of some sort. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_6.png)
     
     I don't have any information as of yet to try to login to this login page. So I will use a nikto scan to explore a litte farther. 
     
1. **Nikto**<br><br>

     After seeing that gobuster didn't bring many results I ran a nikto scan to see if I could find any vulnerabilities.
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_7.png)
     
     I found that there were multiple index files that had the same name. index.html which is typical for the start of a web page and index.php which seemed different. So I added the extension on to the url. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_8.png)
     
     It shows "not found" however it still seems a little weird that there is an extension with .php So I viewed the page source. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_9.png)
     
     The new says that beelzebub is encrypted with md5. So I tried it out.
     
1. **Encrytion**<br><br>

     I used cyberchef but there are several other options that you can search to encrypt and decrypt md5.
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_10.png)
     
     **Tip: If you would like to use the Linux CLI to obtain the md5 hash type $"echo -n beelzebulb | md5sum"
     
     I took the md5 hash and tried to use it as a password. But I realized that hashes are usually added to url links. So I added it onto the end of the url. 
     
     ![step1]({{ site.baseurl }}/images/vulnhubs/beelzebulb/beelzebulb_11.png)
