---
ID: 2941
post_title: >
  Asterix for Banana Pi (FreePBX img file
  for Banana Pi included)
author: Shoaib Ahmed
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/asterix-for-banana-pi-freepbx-img-file-for-banana-pi-included/
published: true
post_date: 2015-01-15 11:07:03
---
<h3>What is Asterix?</h3>
<b>Asterisk</b> is a software implementation of a telephone <a class="mw-redirect" title="Private branch exchange" href="http://en.wikipedia.org/wiki/Private_branch_exchange">private branch exchange</a> (PBX); it was created in 1999 by Mark Spencer of <a title="Digium" href="http://en.wikipedia.org/wiki/Digium">Digium</a>. Like any PBX, it allows attached telephones to make calls to one another, and to connect to other telephone services, such as the public switched telephone network (PSTN) and Voice over Internet Protocol (VoIP) services. Its name comes from the asterisk symbol, *. [Source: <a href="http://en.wikipedia.org/wiki/Asterisk_%28PBX%29">Wikipedia</a>]

Asterisk is like a box of Legos for people who want to create communications applications. It includes all the building blocks needed to create a PBX, an IVR system, a conference bridge and virtually any other communications app you can imagine. [Source: <a href="http://www.asterisk.org/">Official Asterix Website</a>]
<h3>What is Banana Pi?</h3>
<b>Banana Pi </b>is a single-board computer built with ARM Cortex-A7 Dual-core (Allwinner A20 based) CPU and Mali400MP2 GPU, and open source software, Banana Pi can serve as a platform to make lots of applications for different purposes.
<h3>The RasPBX Project</h3>
This is a project dedicated to <a href="http://asterisk.org/" target="_blank">Asterisk</a> and <a href="http://freepbx.org/" target="_blank">FreePBX</a> running on the Raspberry Pi. Later, the Beaglebone folks ported <a href="http://www.raspberry-asterisk.org/about/">RasPBX</a> for the <a href="http://www.beaglebone-asterisk.org/about/">BeagleBone Black (BBB)</a>.
<h3>Asterix for Banana Pi</h3>
Sadly, the RasPBX project doesn't support the Banana Pi yet. I looked everywhere on the net for an Asterix based PBX image for Banana Pi, but looks like no one has done this yet or they did but didn't share . So, I decided to make one myself.

I simply replaced the rootfs on the Banana Pi's Raspbian based image with RasPBX's rootfs. The image should work on any Banana Pi variant with the Allwinner A20 processor (including Banana Pi, Banana Pro and Sinovoip's Banana Pi M1).
<h3>Download links</h3>
The image file is 3.7GB, I am uploading a winrar compressed version that is approximately 437MB . Use a suitable application to un-compress it after download.
<!--
<iframe class="br-right-md" src="http://www.paywithapost.de/dlbutton01.php?id=57e397b9-25fa-4547-8b2f-f53bf83cbc32" name="paytweet_button" width="145px" height="24px" frameborder="no" scrolling="no">

<strong>OR</strong> -->Pay 22.5 USD  (this will support our work)

<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top"><input name="cmd" type="hidden" value="_s-xclick" />
<input name="hosted_button_id" type="hidden" value="TK8S4VWHWF46U" />
<input alt="PayPal - The safer, easier way to pay online!" name="submit" src="https://www.paypalobjects.com/en_US/i/btn/btn_buynowCC_LG.gif" type="image" />
<img src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" alt="" width="1" height="1" border="0" />
<h3>CREDENTIALS</h3>
root/raspberry
<ul>
 	<li>FreePBX Username: asteriskuser</li>
 	<li>FreePBX Password: pi</li>
</ul>
</form>
<h3>Screenshots</h3>
<a href="http://dostmuhammad.com/wp-content/uploads/FreePBX_admin_screen.jpg"><img class="alignleft wp-image-2951 size-medium" src="http://dostmuhammad.com/wp-content/uploads/FreePBX-UI-300x163.png" alt="FreePBX UI" width="300" height="163" /><img class="alignnone wp-image-2950 size-medium" src="http://dostmuhammad.com/wp-content/uploads/FreePBX_admin_screen-300x266.jpg" alt="FreePBX_admin_screen" width="300" height="266" /></a>
<h3>Further  Resources:</h3>
<a href="http://www.raspberrypi.org/documentation/installation/installing-images/">Directions to write the image to SD card</a>

<a href="http://www.raspberry-asterisk.org/">Read Documentation from RasPBX's official website</a>

&nbsp;

PS: I have tested the image and it's working fine. If you are facing any problems with it, feel free to post a comment and I'll be happy to help. :)