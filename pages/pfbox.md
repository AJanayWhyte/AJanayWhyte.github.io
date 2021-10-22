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

![step7]({{ site.baseurl }}/images/pfsense/pfsensee_10.png)<br>
