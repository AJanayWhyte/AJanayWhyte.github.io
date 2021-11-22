---
layout: page
title: InfoSec Prep OSCP
permalink: /oscp/
---

[Click here to download Info Sec Prep: OSCP](https://www.vulnhub.com/entry/infosec-prep-oscp,508/)<br>

Goal: use priviledge escalation to gain root access to the target machine.<br>
Hint: The IP address to the target machine is given right away.<br>
<hr>
Target IP Address: 192.168.1.108
<hr>

1. **The Target Machine**<br><br>
     As the hint states above, we are given the target machine's IP address right away.<br>
     ![step1]({{ site.baseurl }}/images/vulnhubs/oscp/oscp1_1.png)


1.  **Netdiscover**<br><br>
     Even though I know what the target machine's IP address, I still want to verify that I can find the target        machine through my attacking machine.<br>

     ![step2]({{ site.baseurl }}/images/vulnhubs/oscp/oscp2_2.png)

     As we can see, there are 4 ports open. More importantly, two of those ports are 22 - ssh, and 80 - http.<br> 

1. **Nmap**<br><br>
     I ran an nmap command to scan the target network to see what could be revealed.<br>

     ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp3_3.png)

     From the results I see that there are two ports that are open. Port 22 - ssh and port 80 - http. I also see        that there is a robots.txt and a disallow secret.txt.<br>

1. **Port 80 - HTTP**<br><br>
     Now that I know that port 80 is open I typed in the IP address to see what would show up in the browser.<br>
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/oscp/oscp4_4.png)
     
     As I read through the page I see that there is another hint given. I now have the user name.<br>
     
 1. **robots.txt**<br><br>
     From there I went to the robots.txt extension. As found earlier in the nmap scan secret.txt is supposed to be      disallowed. But let's test it anyway.<br>  
        
     ![step5]({{ site.baseurl }}/images/vulnhubs/oscp/oscp5_5.png)
        
 1. **secret.txt**<br><br>
     Now I see why secret.txt was supposed to be disallowed. It looks like there is encoded base64 hidden on this      page. So I will try to use it.<br>  
     
     ![step5]({{ site.baseurl }}/images/vulnhubs/oscp/oscp6_6.png)
     
1. **Base64 Decode**

     There are many ways that base64 can be decoded. I chose to decode it within the CLI using the echo command in      conjunction with the base64 command.<br> 
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/oscp/oscp7_7.png)
     ![step4]({{ site.baseurl }}/images/vulnhubs/oscp/oscp8_8.png)
     
     The base64 decoded and it seems to to be an SSH private key.<br>
     
     ![step4]({{ site.baseurl }}/images/vulnhubs/oscp/oscp9_9.png)
     
1. **Saving the key in a text file**

     Using the cat command I saved the private key inside of a .txt file.<br>
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp10_10.png)
      
1. **SSH**<br><br>
     
     I then used the file that held the key and tried to login as the oscp user to gain access to the target            machine. But it didn't work out to well. So I had to find an alternate route.<br> 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp11_11.png)
     
1. **SSH 2.0**<br><br>
     
     I went back to the original base64 characters that were found from the secret.txt url. I then saved it into a      text file without decoding it first.<br>
 
     ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp12_12.png)
     
     I then use the cat command in conjunction with the tr command and then saved it as a new .txt file. The tr        command is used to remove unneeded spacing and characters inside of the text input into the file. The -d          option deletes characters in the first set from the output. And, '\n' creates a newline after n.<br>
     
    ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp13_13.png)
    
    This then creates a new file. From there I created a new file again but this time decoded the base64 at the       same time. 
     
    ![step3]({{ site.baseurl }}/images/vulnhubs/oscp/oscp14_14.png)
    
    Now that I have a new file with the secret.txt information decoded from base64 I then need to change to permissions so that owner/creater have read and write access but no       one else does. 
1. **Privilege Escalation**<br><br>

     Once I got into SSH with thomas's login information it wasn't allowing me to move around. It seems that the current shell is set to restricted. So after doing a bit of research I found that there was a way to change the restricted status by using vim.

     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_23.png)
     
     After typing the statement in the screen shot press enter and then type :shell, then save and exit. You should now be able to change directories.
     
     I tried to transfer files over to the target machine. But I couldn't get anything to work. I even tried to transfer files through the uploads url. Nothing worked for me. So I had to go back to the drawing board.
     
1. **SCP**<br><br>

     I found a method that uses SCP which allows you to transfer files through the ssh connection. Decided to use Linux exploit suggester to find an ways to exploit the target system. 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_27.png)
     
     I downloaded the suggester onto my machine and used scp to copy it onto the target machine. 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_28.png)
     
     After the copy transfer I saw that the file transfered successfully into the TMP folder on the target machine. 
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_29.png)
      
      I ran the program and it brought back a list of exploits. The list goes from most likely to least likely. I used eBPF_verifier
     
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_31.png)
      
      After finding an exploit. I downloaded it and then used gcc which is a c++ compiler to change the output of the file and then used scp to transfer a copy over to the target machine.
      
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_34.png)
      
      Once I had access to the file on the target computer I then ran the exploit and the execution was successful. 
      
      ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_38.png)
      
1. **Root**<br><br>

     After the exploit ran on the target machine I used the id command to see who I was. I DID IT! I AM ROOT!
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_39.png)
     
     We now need to use a python script to traverse into the root folder
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_40.png)
     
     After using the python script I was able to change into the root directory and list it's contents. 
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_41.png)
     
     I finally found the root flag and opened it up. WE FOUND THE FLAG!
     
     ![step3]({{ site.baseurl }}/images/vulnhubs/funbox4/fb4_42.png)
      
