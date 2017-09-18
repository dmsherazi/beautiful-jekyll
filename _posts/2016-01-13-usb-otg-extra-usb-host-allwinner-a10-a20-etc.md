---
ID: 3451
post_title: >
  USB OTG as an Extra USB Host in
  Allwinner A10, A20 etc
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/usb-otg-extra-usb-host-allwinner-a10-a20-etc/
published: true
post_date: 2016-01-13 17:03:42
---
<strong>USB OTG</strong> port on Allwinner SoC based boards is a very useful tool. It can be used to flash an image to the flash memory or connect to a Host PC and making the board to act as a device.

Although there are many scenarios where USB OTG is useful, at times it is more useful to have an extra USB HOST on the board. All the settings of hardware configurations of allwinner SoCs are stored in a file named ` script.bin` that is compiled from a text file called fex file.We can learn more about the fex file from <a title="Sunxi Wiki" href="http://linux-sunxi.org/" target="_blank">Sunxi Wiki</a> in the <a title="Fex Guide" href="http://linux-sunxi.org/Fex_Guide#12.1_.5Bdisp_init.5D" target="_blank">Fex Guide</a>.

A <strong>FEX</strong> file defines various aspects of how the SoC works. It configures the GPIO pins and sets up DRAM, Display, etc parameters.

Each line consists of a key = value pair combination under a [sectionheader]. All three, [<strong>sectionheader</strong>], key and value are case-sensitive. For comments a semi-colon (<strong>;</strong>) is used and everything following a semi-colon is ignored. The chip does not parse a textual version of a fex file, it gets cleaned and compiled by a fex-compiler. A reverse engineerd open source version exists in the sunxi-tools repository. Also a de-compiler which takes a binary script.bin and creates a textual script.fex. Usually, script.bin can be found on the nanda boot partition on A10 devices.
<h4><b>Changing script.bin file without removing the microSD card</b></h4>
The tools for script.bin changing are located in /opt/sunxi-tools directory:
<pre>  # cd /opt/sunxi-tools
  # ./chscr.sh
</pre>
This will convert script.bin file from sdcard to script.fex file and the file will be opened using nano editor. Now you can change the board modules and parameters, save the changes ("CTRL"+"X"; confirm with "Y") and exit ("CTRL"+"X" again) from nano editor.
<pre>  # ./wrscr.sh
</pre>
this will convert script.fex to script.bin and the script.bin file will be written to sdcard.
<pre>  reboot
</pre>
Reboot the board and the new settings would be enabled.
<h4><b>Changing script.bin file by removing the microSD card</b></h4>
The biggest part of the board configuration might be edited, changed or improved in a file called script.bin

The script.bin file can usually be found in the main directory of a microSD card prepared with official Debian image. The folder containing the script can be inspected under both Windows, Linux or Mac.

You can't directly edit binary file so you would need to convert it to text format (it is called fex in this case), then edit the parameters via a text editor and finally switch it back to binary format.

IMPORTANT! ADJUSTING SCRIPT.BIN WITH IMPROPER VALUES MIGHT BREAK YOUR DEBIAN IMAGE AND IT IS ALWAYS RECOMMENDED TO KEEP A BACK-UP OF YOUR DEFAULT SCRIPT.BIN

To convert back and forth the script.bin you might use different tools. You can find Windows tools here: <a class="external text" href="https://github.com/OLIMEX/OLINUXINO/tree/master/SOFTWARE/fex-bin-convertor-windows" rel="nofollow">SUNXI TOOLS FOR WINDOWS</a> . For Linux convertors please check the sunxi tools here: <a class="external text" href="https://github.com/linux-sunxi/sunxi-tools" rel="nofollow">SUNXI TOOLS</a>
<h4>Editing Fex File for USB OTG</h4>
Now open the Fex file and locate the USB section.
<pre>;——————————————————————————- 
;[usbc0]:  The configuration of controller 0 
;usb_used: Enable bit. If USB is enabled or not. 1: enable; 0: disable. 
;usb_port_type: Type of USB port. 0：device only;1：host only;2:OTG 
;usb_detect_type: Detect type. 0: Not detect; 1: detect vbus/id; 2: Detect id/dpdm
;——————————————————————————- 
;——————————————————————————- 

;——————————————————————————-
[usbc0]
usb_used = 1 
usb_port_type = 0 
usb_detect_type = 0 
usb_id_gpio = port:PH04&lt;0&gt;&lt;1&gt;&lt;default&gt;&lt;default&gt; 
usb_det_vbus_gpio = “axp_ctrl” 
usb_drv_vbus_gpio = port:PB09&lt;1&gt;&lt;0&gt;&lt;default&gt;&lt;0&gt; 
;usb_restrict_gpio = port:PH00&lt;1&gt;&lt;0&gt;&lt;default&gt;&lt;0&gt; 
usb_host_init_state = 0 
usb_restric_flag = 0 
usb_restric_voltage = 3550000 
usb_restric_capacity= 5</pre>
We just need to change usb_port_type from 0 to 1 to make it a USB host.
<h4>Converting fex to script.bin:</h4>
The following commands are executed at sunxi-tools directory:
<pre class="crayon-toolbar" data-settings=" mouseover overlay hide delay">$./fex2bin script.fex &gt;script.bin
$sudo cp script.bin /boot/script.bin
$sudo umount /boot</pre>
<div class="crayon-toolbar" data-settings=" mouseover overlay hide delay">Now restart the board and you can use USB OTG as USB host.</div>