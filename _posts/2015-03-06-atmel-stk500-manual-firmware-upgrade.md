---
ID: 3074
post_title: Atmel STK500 Manual Firmware Upgrade
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/atmel-stk500-manual-firmware-upgrade/
published: true
post_date: 2015-03-06 15:05:50
---
Atmel Studio will automatically detect any old Atmel STK500 firmware version and request the user to upgrade the firmware. If for some reason the upgrade fails (the serial cable is detached during upgrade, the power goes out, …) the next time the Atmel Studio tries to connect to the STK500, the board will not be detected and the automatic upgrade procedure will not start.

Following is a procedure on how to manually upgrade an STK500 board. This procedure should work in all cases. The procedure is slightly different for AVR Studio 4 and AVR Studio 5<span id="more-881"></span>
<div>
<div>
<div>
<div>
<h3>AVR Studio 4</h3>
</div>
</div>
</div>
<div>
<ol type="1">
	<li>Power off the Atmel STK500</li>
	<li>On the STK500, push the <em>PROGRAM</em> button while turning on the power.</li>
	<li>Make sure there is a serial connection between the PC and the STK500 DSUB9 marked <em>RS232 CTRL</em></li>
	<li>Start AVR Studio 4, and from the Tools menu start the program ‘Avr Prog’</li>
	<li>Locate the firmware upgrade hex-file <em>stk500.ebn</em> by pushing the Browse button in the Avr Prog Hex File window. The path for the <em>stk500.ebn</em> for a normal AVR Studio 4 installation is <code>C:Program FilesAtmelAVR ToolsSTK500STK500.ebn</code>.</li>
	<li>Push the Program button in the <em>Avr Prog</em> Flash window. A progress bar will now appear while showing additional information messages. Wait until the verify operation is finished.</li>
	<li>Close the <em>Avr Prog</em> program</li>
	<li>Power off and on the STK500 PCB. The STK500 is now ready to be used with the new firmware.</li>
</ol>
</div>
</div>
<div>
<div>
<div>
<div>
<h3><a id="stk500.section.rgz_iud_lc"></a>Atmel Studio and AVR Studio 5</h3>
</div>
</div>
</div>
The <em>AVR Prog</em> program is not distributed with the Atmel Studio installer. There is a separate installer for a set of <a href="http://www.atmel.no/beta_ware/AVRCommandLineTools/AVRCommandLineTools.zip" target="_top">command line tools</a> which also includes <em>AVR Prog</em>.
<div>
<ol type="1">
	<li>Make sure the <em>command line tools</em> are installed</li>
	<li>Power off the Atmel STK500</li>
	<li>On the STK500, push the <em>PROGRAM</em> button while turning on the power.</li>
	<li>Make sure there is a serial connection between the PC and the STK500 DSUB9 marked <em>RS232 CTRL</em></li>
	<li>Start ‘AvrProg.exe’. The default installation location is <code>C:Program FilesAtmelAVR ToolsAvrProgAvrProg.exe</code> or <code>C:Program Files (x86)AtmelAVR ToolsAvrProgAvrProg.exe</code> on 64-bit OS.</li>
	<li>Locate the firmware upgrade hex-file <em>stk500.ebn</em> by pushing the Browse button in the Avr Prog Hex File window. The path for the <em>stk500.ebn</em> for a normal Atmel Studio installation is <code>C:Program Files (x86)AtmelAVR Studio 6.0toolsSTK500STK500.ebn</code>.</li>
	<li>Push the Program button in the <em>Avr Prog</em> Flash window. A progress bar will now appear while showing additional information messages. Wait until the verify operation is finished.</li>
	<li>Close the <em>Avr Prog</em> program</li>
	<li>Power off and on the STK500 PCB. The STK500 is now ready to be used with the new firmware.</li>
</ol>
</div>
</div>