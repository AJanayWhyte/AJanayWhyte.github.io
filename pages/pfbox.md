---
layout: page
title: Pfsense Configuration with VirtualBox
permalink: /pfbox/
---
<hr>
### Table of Contents<br>
<a href="{{ site.baseurl }}/setup">Virtual Machine Configuration</a><br>
<hr>

Follow these instructions to help configure your Pfsense for Virtualbox.

You can find the link to download Pfsense [here](https://www.pfsense.org/download/).

#### Step 1:

In order for you to download the appropriate file to import into VirtualBox, make the appropriate selections inside of the downloader box. Once your file is downloaded use a program such as 7zip to extract the .iso file.

![step1]({{ site.baseurl }}/images/pfsense/pfsensee_2.png){:height="50%" width="50%"}<br>

#### Step 2:

Once you have your .iso file of pfsense, head over to VirtualBox Manager. From here you can either select Machine menu and new. Or the blue new button to the right. 

![step2]({{ site.baseurl }}/images/pfsense/pfsensee_3.png)<br>

#### Step 3:

We now have to create a new virtual machine. Choose a new name for your pfsense machine. I chose pfsense1. Change the type to BSD and change the version to FreeBSD (64-bit). Click the yes button.

![step3]({{ site.baseurl }}/images/pfsense/pfsensee_4.png){:height="50%" width="50%"}<br>

#### Step 4:

Click next through the screens until it asks you to press the create button.

![step4]({{ site.baseurl }}/images/pfsense/pfsensee_6.png){:height="50%" width="50%"}<br>

#### Step 5:

Now change the selection to VMDK to create a virtual machine hard disk.

![step5]({{ site.baseurl }}/images/pfsense/pfsensee_7.png){:height="50%" width="50%"}<br>

#### Step 6:

Continue to move through the screens until you are able to adjust the file location and size of the hard disk. I chose 20GB but it is completely your choice. 

![step6]({{ site.baseurl }}/images/pfsense/pfsensee_9.png){:height="50%" width="50%"}<br>

#### Step 7:

Now that we have created a new pfsense virtual machine, select the machine so that it turns blue and click the settings button on the upper right.

![step7]({{ site.baseurl }}/images/pfsense/pfsensee_10.png)<br>

#### Step 8:

Now we will setup the network portion of Pfsense by clicking network on the left side of the window.

![step8]({{ site.baseurl }}/images/pfsense/pfsensee_11.png)<br>

#### Step 9:

We will set up two different network adapters. For adapter one change the attached to drop down to Bridged Adapter. This is going to allow whatever internet connection that is going through Pfsense to to connect to the second adapter.

![step9]({{ site.baseurl }}/images/pfsense/pfsensee_12.png)<br>

#### Step 10:


![step10]({{ site.baseurl }}/images/pfsense/pfsensee_13.png)<br>
