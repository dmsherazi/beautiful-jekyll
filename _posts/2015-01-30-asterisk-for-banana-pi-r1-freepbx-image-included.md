---
ID: 2957
post_title: >
  Asterisk for Banana Pi R1 (FreePBX Image
  included)
author: Shoaib Ahmed
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/asterisk-for-banana-pi-r1-freepbx-image-included/
published: true
post_date: 2015-01-30 15:29:24
---
After doing the <a title="Asterix for Banana Pi (FreePBX img file for Banana Pi included)" href="http://dostmuhammad.com/blog/asterix-for-banana-pi-freepbx-img-file-for-banana-pi-included/">FreePBX Asterisk Image for Banana Pi</a>, I was asked by <a href="http://www.sinovoip.com.cn/">SINOVOIP (Banana Pi Manufacturer) </a>to do an Asterisk Image for their router board, i.e. the Banana Pi R1. SINOVOIP has been very kind to send me a complimentary BPi-R1 for testing and developing.

It took me some time to get this done, but the image is finally ready. This image differs from my earlier Banana Pi Asterisk image in that, the earlier image was created by simply replacing the rootfs of a <a href="http://www.lemaker.org/bananapro/141-271/raspbian_for_bananapro.html">Raspbian based BPi Image</a>, with <a href="http://www.raspberry-asterisk.org/">RasPBX Image's</a> rootfs. However, this time I have actually been able to compile Asterisk on the latest Bananian Image for R1. This means that you can now have a powerful, complete and rather flexible Asterisk 11 (upgradable to 12!) desktop system with FreePBX, running on the BPi-R1. Further, Bananian offers lightening fast boot and load times with remarkable performance. (You can compare the speed with my earlier RasPBX based Image to see for yourself.)

The image comes preloaded with Asterisk 11, along with most of the standard FreePBX modules. Upgrading to Asterisk 12 should be pretty easy.

<strong>Credentials:</strong>
<ul>
	<li>Login: root</li>
	<li>Password: root</li>
	<li>FreePBX Username: asteriskuser</li>
	<li>FreePBX Password: pi</li>
</ul>
Note: I have tested this image (before and after upgrading to Asterisk 12) successfully with a BPi-R1 for SIP (using Android devices running <a href="http://www.zoiper.com/en">Zoiper</a>), along with video calling. Please be aware that 2 extensions (made during testing) already exist in the image and can be removed (I somehow forgot to delete them ;)). Also note that video calling is disabled by default and needs to be enabled from the pbx settings.
<h3>DOWNLOAD :</h3>
<!--<iframe width="145px" height="24px" src="http://www.paywithatweet.com/dlbutton01.php?id=608dc979-4f50-4317-b139-136eb3026c83" class="br-right-md" name="paytweet_button" scrolling="no" frameborder="no">
<strong>OR</strong> -->Pay 22.50 USD  (this will support our work)

<form action="https://www.paypal.com/cgi-bin/webscr" method="post" target="_top"><input name="cmd" type="hidden" value="_s-xclick" />
<input name="hosted_button_id" type="hidden" value="BGBDHLD6AM2VE" />
<input alt="PayPal - The safer, easier way to pay online!" name="submit" src="https://www.paypalobjects.com/en_US/i/btn/btn_buynowCC_LG.gif" type="image" />
<img src="https://www.paypalobjects.com/en_US/i/scr/pixel.gif" alt="" width="1" height="1" border="0" /></form>Download both files and then un-rar using WinRar or any other appropriate program