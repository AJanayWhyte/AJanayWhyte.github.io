---
layout: page
title: Funbox CTF - Medium
permalink: /funbox4/
---
[Click here to download Funbox CTF](https://www.vulnhub.com/entry/funbox-ctf,546/)<br>

Funbox CTF comes from a series of 11 boxes. 

Goal: use priviledge escalation to gain root access to the target machine.
Hint: Case sensitive with using Nikto and need a minimum of 15 mins to find the user.
<hr>
Target Mac address: 08:00:27:4f:b1:d6
<hr>

1. **Netdiscover**<br><br>
     We know our Target machine's Mac address. We need to do a netdiscover to find the IP address to the machine. 

     ![step1]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_1.png)


1.  **Nmap**<br><br>
     Now that we have identified our target IP we should run an nmap scan to see what information                       we can find on the target network. 

     ![step2]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_2.png)

     As we can see, there are 4 ports open. More importantly, two of those ports are 22 - ssh, and 80 - http. 

1. **Port 80**<br><br>
     Let's see if we can gain access to a url by going to http://192.168.1.19 .

     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_3.png)

     The url takes us to the Apache2 Ubuntu Default server page.

1. **Dirsearch**<br><br>
     I used Dirsearch to see if I could find any hidden directories attached to the url.
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_4.png)
     
     Looks like there is a ROBOTS.TXT. After trying to gain access to several times. I remembered the hint that        was given earlier. Case Sensitive. Trying robots.txt with all capital letters as it shows in the dirsearch        finding. I finally found results. 
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_5.png)
     
     Looks like there is an uploads directory. When I scroll down to the bottom of the page it looks like there is      a hash of some sort. 
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_6.png)
     
 1. **Dirsearch - with hash**<br><br>
     I took the hash that was discovered and added it to the end of the IP url. And     becuase I only used .txt extension during the first search I        added .php and .html as well. 
        
     ![step5]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_7.png)
        
     The new search has brought back several extension that include both php and html. Two of which include the newly found uploads directory. 
     
     Once I gained access to the uploads url I see that there is a browse and upload button. I also saw that the Dirsearch had an uploads.php so I'm going to assume that I should upload a .php file. So let's create a backdoor in.
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_8.png)
     
 1. **Php Reverse Shell**<br><br>

     In order for us to gain access in to the webserver we will be using php-reverse-shell to create a backdoor. If you're not sure where to find this file try using the command "locate php-reverse-shell" and it should pop up. 
     
     ![step5]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_43.png)
     ![step5]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_44.png)

