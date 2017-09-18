---
ID: 3078
post_title: >
  Firmware upgrade for SIM900 GSM/GPRS
  modem
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/firmware-upgrade-for-sim900-gsmgprs-modem/
published: true
post_date: 2015-03-17 06:43:49
---
In this post we will learn how to update the firmware.
<h3>Requirements</h3>
<ul>
	<li><a href="http://dostmuhammad.com/wp-content/uploads/Simcom_-_sim900_Customer_flash_loader_V1.01.rar">Simcom_-_sim900_Customer_flash_loader_V1.01</a></li>
	<li>Sim900 Baord with serial or USB interface to connect to PC.</li>
	<li>A Firmware of SIM900 can be found <a title="sim900-firmware-update-tutorials-appnotes" href="http://dostmuhammad.com/blog/sim900-firmware-update-tutorials-appnotes/">here</a>.</li>
</ul>
<h5>You can use AT Command “<strong>AT+GSV</strong>” to check the current version of the Firmware.</h5>
<h3><span id="more-888"></span>.Cautions</h3>
<ul>
	<li>After the upgrate, the baurate of GPRS will 0(auto baudrate); Make sure you use “AT+IPR=xxx” to set the baudrate if you are not using autobaudrate.</li>
	<li>If you are not able to communicate with sim900 after flashing new firmware check this post <a title="GSM Modem/Module not responding to AT commands after firmware Upgrade??" href="http://dostmuhammad.com/blog/gsm-modemmodule-not-responding-to-at-commands-after-firmware-upgrade/">GSM Modem/Module not responding to AT commands after firmware Upgrade?? </a></li>
</ul>
<h3>How to</h3>
Application note <a href="http://dostmuhammad.com/wp-content/uploads/AN_SIM900_Update-Tool_UGD_V1.01.pdf">AN_SIM900_Update Tool_UGD_V1.01</a> from simcom explains the process.

Step1

Download Simcom – <a href="http://dostmuhammad.com/wp-content/uploads/Simcom_-_sim900_Customer_flash_loader_V1.01.rar">sim900 Customer flash loader V1.01</a>; Unzip the Simcom – sim900 Customer flash loader V1.01.

Step2

Connect your SIM900 board to your PC;

Step3

Open the executable file “Simcom – sim900 Customer flash loader V1.01″, it will show  window like the one below
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/4/4e/Up2.jpg" alt="Up2.jpg" width="476" height="459" />
<p class="wp-caption-text">Step 3</p>

</div>
Step4

Select the right COM port(in my case is COM12), and the default value of Speed is 460800(baudrate), and 460800 is OK from my experience.

Step5

Click the <strong>Browse</strong> to select the downloaded firmware(in my case is 1137B03SIM900M64_ST_MMS ). You can see  window like the one below
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/2/2d/Up3.jpg" alt="Up3.jpg" width="485" height="475" />
<p class="wp-caption-text">Step 5</p>

</div>
Step6

Click the <strong>START</strong> button to download, you will see  window like the one below
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/3/3d/Up4.jpg" alt="Up4.jpg" width="479" height="461" />
<p class="wp-caption-text">Step 6</p>

</div>
Step7

Now <strong>Switch Off and then Switch ON</strong> GPRS Board .
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/5/51/Up5.jpg" alt="Up5.jpg" width="476" height="537" />
<p class="wp-caption-text">Step 7</p>

</div>
Step8

When the tool is erasing the flash, you will see the window like the one below:(Step9 may last a few minutes)

If fail, you can try another <em><strong>Speed</strong></em>(baudrate),and do it all again.
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/9/97/Up6.jpg" alt="Up6.jpg" width="477" height="463" />
<p class="wp-caption-text">Step 8</p>

</div>
Step9

The whole download process needs about 4 minutes; After the download, you will see window like this
<div class="wp-caption alignnone"><img src="http://web.archive.org/web/20121216042335im_/http://www.geekonfire.com/wiki/images/3/34/Up7.jpg" alt="Up7.jpg" width="475" height="463" />
<p class="wp-caption-text">Step 9</p>

</div>
When you see <strong>Download done</strong>, congratulations that you have upgrade the firmware successfully.