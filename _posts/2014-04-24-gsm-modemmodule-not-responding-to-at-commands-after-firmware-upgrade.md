---
ID: 2611
post_title: >
  GSM Modem/Module not responding to AT
  commands after firmware Upgrade??
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/gsm-modemmodule-not-responding-to-at-commands-after-firmware-upgrade/
published: true
post_date: 2014-04-24 18:05:21
---
I get a lot of queries about this issue, so I thought I should write a small post about it. For example the latest one was
<blockquote>Hello Muhammad,
I recently update SIM900 to firmware 1137B12SIM900M64_ST.cla using “Simcom – sim900 Customer flash loader V1.01″ at the baud rate 1498000. Everything went perfectly like but after I restart the module I get “þIIIIþþþ” response from SIM900 at 115200 baud rate, I could not get any AT commands working. Kindly do help me.</blockquote>
Some modems support <strong>AutoBaud</strong> by default. Auto Baud feature allows the modem to be used with any baud rate, and for this to be used the Modem waits for a input string <code>“ATr”</code> it uses this string to detect the baud rate being used. As the manual describes the modem when in Auto Baud will be looking for this string after it is powered and this should be in CAPS otherwise modem wont be able to detect the correct baud rate. Sim900 has the auto baud by default. Some modems don not support Auto Baud so for these modems after the firmware has been updated, you should use the default baud rate, <strong>9600 </strong>and<strong> 115200</strong> are the most common.

if you want to fix or change the baud rate you should use the AT+IPR command. For example if you need to fix it to 4800.
<pre> AT+IPR=4800r</pre>