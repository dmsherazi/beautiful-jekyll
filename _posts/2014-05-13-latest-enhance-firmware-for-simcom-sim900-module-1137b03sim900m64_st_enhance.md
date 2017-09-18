---
ID: 2671
post_title: >
  latest enhance firmware for SIMCOM
  SIM900 module
  (1137B03SIM900M64_ST_ENHANCE )
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/latest-enhance-firmware-for-simcom-sim900-module-1137b03sim900m64_st_enhance/
published: true
post_date: 2014-05-13 10:37:49
---
In continuation to my <a title="a collection of firmwares app notes and guides for simcom" href="http://dostmuhammad.com/blog/a-collection-of-firmwares-app-notes-and-guides-for-simcom/">posts regarding firmwares for SIMCOM modules</a> , here is the <a href="https://www.dropbox.com/s/f215rir5ftytzpj/1137B03SIM900M64_ST_ENHANCE%20%281%29.cla">latest firmware for sim900</a>.  It supports the  following along with other standard  features
<ul>
	<li>DTMF</li>
	<li>Jamming detection</li>
	<li>MMS</li>
	<li>GSM location</li>
	<li>Email</li>
</ul>
<!--more-->

The new features and improvements compared to the previous version can be found in the Release notes attached
<blockquote>
<h3><strong>[New Features]</strong></h3>
<ul>
	<li>1. Added NTP function.</li>
	<li>2. Added "AT+CMMSTYPECTL" to set the assembling method of MMS to be sent. 0 is the default value which indicates application/vnd.wap.multipart.mixed method, and 1 is for application/vnd.wap.multipart.related method.</li>
	<li>3. Added "AT+FTPRENAME" command to rename the specified file of remote machine.</li>
	<li>4. Added "AT+FTPMDTM" command to get the last modification timestamp of specified file on the remote machine.</li>
	<li>5. Added "AT+SJDEDV" command to set threshold for entering and exiting JD condition.</li>
	<li>6. Added "AT+CQUICKPDP" to adjust T3380 and T3390.</li>
</ul>
<h3><strong>[Improved Features] </strong></h3>
<ul>
	<li>1. Fixed the spelling mistake of the abbreviation of "October" when sending a email by using SMTP.</li>
	<li>2. Solved the problem when processing the test command and read command of CSMINS it doesn't return the result in a new line.</li>
	<li>3. Solved the problem that the net light will not be turned off when POWERKEY is pulled to high level.</li>
	<li>4. Solved the problem that CELLID is not correct after using CELLLOCK command.</li>
	<li>5. Added "AT+FTPQCLOSE" command, when "AT+FTPQCLOSE=1" is set, the problem that it takes a long time to wait for the return result of FTP download operation can be solved.</li>
	<li>6. Solved the problem that some websites cannot be obtained by HTTP GET method.</li>
</ul>
</blockquote>
&nbsp;
<h3>Download:</h3>
<ul>
	<li><a href="https://www.dropbox.com/s/f215rir5ftytzpj/1137B03SIM900M64_ST_ENHANCE%20%281%29.cla">1137B03SIM900M64_ST_ENHANCE</a></li>
	<li><a href="https://www.dropbox.com/s/llb4dxa6tri938h/NDA_SIM900M64_ST_ENHANCE%20Firmware%20Release%20Note%20%282%29.pdf">Release Notes</a></li>
</ul>
<h3>For other firmwares :</h3>
<a href="http://wp.me/p2D6cb-Fr">http://wp.me/p2D6cb-Fr</a>
<a href="http://wp.me/p2D6cb-Gh">http://wp.me/p2D6cb-Gh</a>
<a href="http://wp.me/p2D6cb-Gk">http://wp.me/p2D6cb-Gk</a>