---
layout: page
title: Oracle - Virtualbox Configuration
permalink: /vbox/
---
<hr>
### Table of Contents<br>
<a href="{{ site.baseurl }}/setup">Virtual Machine Configuration</a><br>
<hr>

Follow these instructions to help configure your Oracle - Virtualbox.

#### Step 1:
Before making any changes to your virtualbox settings, make sure that your machine is powered off.

![step1]({{ site.baseurl }}/images/VM/vbox/vboxx_10.png)<br>

#### Step 2:
Then click file and then preferences.
 
![step2]({{ site.baseurl }}/images/VM/vbox/vboxx_6.png)<br>

#### Step 3:
A new window will open up. Select network on the left hand side. Then click the green plus sign on the right hand side. 

![step3]({{ site.baseurl }}/images/VM/vbox/vboxx_7.png)<br>

#### Step 4:
A new nat network will appear with a check in the active box. Press the OK button. 

![step4]({{ site.baseurl }}/images/VM/vbox/vboxx_8.png)<br>

#### Step 5:
A new window will open. This window will show you the new nat network's name, along with the CIDR IP address range. Both fields can be changed if you would like. For now, let's keep it the same. Press the OK button.

![step5]({{ site.baseurl }}/images/VM/vbox/vboxx_9.png)<br>

#### Step 6:
This will bring you back to the original window. Press the machine menu selection and then press settings. 

![step6]({{ site.baseurl }}/images/VM/vbox/vboxx_2.png)<br>

#### Step 7:
Select Network on the left hand side. 

![step7]({{ site.baseurl }}/images/VM/vbox/vboxx_3.png)<br>

#### Step 8:
Click to check the "enable Network adapter box. 

![step8]({{ site.baseurl }}/images/VM/vbox/vboxx_4.png)<br>

#### Step 9:
Lastly, select the drop down window for attached to and select Nat Network. This will add the newly created nat network that we created a few steps ago. From there select OK. We're all done!

![step9]({{ site.baseurl }}/images/VM/vbox/vboxx_5.png)<br>

### Congrats you have configured your VirtualBox!
