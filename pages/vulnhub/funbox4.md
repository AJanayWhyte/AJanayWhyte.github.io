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
     
     *Note: the current target IP address is different due to stopping and restarting the box.*
     
 1. **Php Reverse Shell**<br><br>

     In order for us to gain access in to the webserver we will be using php-reverse-shell to create a backdoor. If you're not sure where to find this file try using the command "locate php-reverse-shell" and it should pop up. 
     
     ![step5]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_43.png)
     
     In order for the file to work properly we need to edit the information inside the file. Make a copy of the current file so you can keep your original and then edit the file using nano. 
     
     ![step5]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_44.png)
     
     Once inside of the php file we need to change the ip address and the port number. The ip address should be your own machine's ip address. choose a port number for the file to use. I chose port number 8888.

1. **Uploading your file**

     In order to verify that our backdoor file is working we need to set up a port listener by using netcat
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_10.png)
     
     *Note: the current listening port number is different due to stopping and restarting the box. It should still work using the previous port.*
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_9.png)
     
     Once you upload your new php file you should get a confirmation that it was successful.
    
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_12.png)
     
     Once the file is uploaded the port listener should change to something similar to the image above. This will also give you access to the target's network. 
     
1. **Traversing the target network**

     Now that we are in, let's see what we can find. The first thing I did was a list command to see what type of files show up immediately. 
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_13.png)

     Right away I found a hint.txt file. I opened it to see what was inside. 
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_14.png)
      
      As you can see it a bunch of nothing. However, there is one hint that may help us out. The hint mentions rockyou.txt and sed which is used for searching, replacing, and inserting/deleting text in a .txt document. 
      
      Let's keep looking to see what else we find. I went farther into the directories and saw that there were two sub directories under user names of Anna and thomas. When opening anna's directory I didn't find anything. But, under thomas there is a file called .todo . 
      
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_17.png)
      
     When I opened the .todo file it was essentially a todo list just as listed. Number 7 says that thomas needs to add an exclamation mark to his password. Now we know that he has an exclamation mark in his password. 
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_18.png)
      
1. **Rockyou.txt & sed**<br><br>
     
     We are going to use both rockyou.txt and sed to create a new wordlist that will have passwords containing exclamation marks. Use the command in the screenshot and name your new wordlist. If you can't find rockyou.txt try using locate. 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_19.png)
     
     As you can see, if you open the newly created wordlist file all of the passwords inside will all have exclamation marks. We will use this to try and crack the password to login for thomas. 
     
1. **Hydra**<br><br>
     
     We will now take the new wordlist that we created and use Hydra to try to crack the password for thomas's login. 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_20.png)
     
     There are a few different things we are using to ensure that we can crack the password. 1. -l for login, 2. -p for password, the target ip address to use for ssh. As you can see the new wordlist is attached to -p as well as thomas's name for -l. This produces the password along with the login a little bit farther down. We cracked it! Now let's login as thomas!
     
     
