---
ID: 3340
post_title: >
  Getting power and battery info from
  AXP209
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/getting-power-and-battery-info-from-axp209/
published: true
post_date: 2015-06-24 16:23:34
---
Here is a script that gives some info about battery (when one is plugged)

I think that this page has mistakes (<a href="http://linux-sunxi.org/AXP209#Spec_Sheets">http://linux-sunxi.org/AXP209#Spec_Sheets</a>) because discharging and charging current are inverted.
<pre>#!/bin/sh
# This program gets the battery info from PMU
# Voltage and current charging/discharging
#
# Nota : temperature can be more than real because of self heating
#######################################################################
# Copyright (c) 2014 by RzBo, Bellesserre, France
#
# Permission is granted to use the source code within this
# file in whole or in part for any use, personal or commercial,
# without restriction or limitation.
#
# No warranties, either explicit or implied, are made as to the
# suitability of this code for any purpose. Use at your own risk.
#######################################################################

# force ADC enable for battery voltage and current
i2cset -y -f 0 0x34 0x82 0xC3

################################
#read Power status register @00h
POWER_STATUS=$(i2cget -y -f 0 0x34 0x00)
#echo $POWER_STATUS

BAT_STATUS=$(($(($POWER_STATUS&amp;0x02))/2))  # divide by 2 is like shifting rigth 1 times
#echo $(($POWER_STATUS&amp;0x02))
echo "BAT_STATUS="$BAT_STATUS
# echo $BAT_STATUS

################################
#read Power OPERATING MODE register @01h
POWER_OP_MODE=$(i2cget -y -f 0 0x34 0x01)
#echo $POWER_OP_MODE

CHARG_IND=$(($(($POWER_OP_MODE&amp;0x40))/64))  # divide by 64 is like shifting rigth 6 times
#echo $(($POWER_OP_MODE&amp;0x40))
echo "CHARG_IND="$CHARG_IND
# echo $CHARG_IND

BAT_EXIST=$(($(($POWER_OP_MODE&amp;0x20))/32))  # divide by 32 is like shifting rigth 5 times
#echo $(($POWER_OP_MODE&amp;0x20))
echo "BAT_EXIST="$BAT_EXIST
# echo $BAT_EXIST

################################
#read Charge control register @33h
CHARGE_CTL=$(i2cget -y -f 0 0x34 0x33)
echo "CHARGE_CTL="$CHARGE_CTL
# echo $CHARGE_CTL


################################
#read Charge control register @34h
CHARGE_CTL2=$(i2cget -y -f 0 0x34 0x34)
echo "CHARGE_CTL2="$CHARGE_CTL2
# echo $CHARGE_CTL2


################################
#read battery voltage	79h, 78h	0 mV -&gt; 000h,	1.1 mV/bit	FFFh -&gt; 4.5045 V
BAT_VOLT_LSB=$(i2cget -y -f 0 0x34 0x79)
BAT_VOLT_MSB=$(i2cget -y -f 0 0x34 0x78)

#echo $BAT_VOLT_MSB $BAT_VOLT_LSB

BAT_BIN=$(( $(($BAT_VOLT_MSB &lt;&lt; 4)) | $(($(($BAT_VOLT_LSB &amp; 0xF0)) &gt;&gt; 4)) ))

BAT_VOLT=$(echo "($BAT_BIN*1.1)"|bc)
echo "Battery voltage = "$BAT_VOLT"mV"

###################
#read Battery Discharge Current	7Ah, 7Bh	0 mV -&gt; 000h,	0.5 mA/bit	FFFh -&gt; 4.095 V
BAT_IDISCHG_LSB=$(i2cget -y -f 0 0x34 0x7B)
BAT_IDISCHG_MSB=$(i2cget -y -f 0 0x34 0x7A)

#echo $BAT_IDISCHG_MSB $BAT_IDISCHG_LSB

BAT_IDISCHG_BIN=$(( $(($BAT_IDISCHG_MSB &lt;&lt; 4)) | $(($(($BAT_IDISCHG_LSB &amp; 0xF0)) &gt;&gt; 4)) ))

BAT_IDISCHG=$(echo "($BAT_IDISCHG_BIN*0.5)"|bc)
echo "Battery discharge current = "$BAT_IDISCHG"mA"

###################
#read Battery Charge Current	7Ch, 7Dh	0 mV -&gt; 000h,	0.5 mA/bit	FFFh -&gt; 4.095 V
BAT_ICHG_LSB=$(i2cget -y -f 0 0x34 0x7D)
BAT_ICHG_MSB=$(i2cget -y -f 0 0x34 0x7C)

#echo $BAT_ICHG_MSB $BAT_ICHG_LSB

BAT_ICHG_BIN=$(( $(($BAT_ICHG_MSB &lt;&lt; 4)) | $(($(($BAT_ICHG_LSB &amp; 0xF0)) &gt;&gt; 4)) ))

BAT_ICHG=$(echo "($BAT_ICHG_BIN*0.5)"|bc)
echo "Battery charge current = "$BAT_ICHG"mA"
</pre>
<strong>this script gives the AC power status :</strong>
<pre>#!/bin/sh
# This program gets the power status (AC IN or BAT) for pcDuino3
# I2C interface with AXP209
#
#######################################################################
# Copyright (c) 2014 by RzBo, Bellesserre, France
#
# Permission is granted to use the source code within this
# file in whole or in part for any use, personal or commercial,
# without restriction or limitation.
#
# No warranties, either explicit or implied, are made as to the
# suitability of this code for any purpose. Use at your own risk.
#######################################################################

#read Power status register @00h
POWER_STATUS=$(i2cget -y -f 0 0x34 0x00)
#echo $POWER_STATUS

# bit 7 : Indicates ACIN presence 0: ACIN does not exist; 1: ACIN present
#echo "bit 7 : Indicates ACIN presence 0: ACIN does not exist; 1: ACIN present"
#echo "bit 2 : Indicates that the battery current direction 0: battery discharge; 1: The battery is charged"

AC_STATUS=$(($(($POWER_STATUS&amp;0x80))/128))  # divide by 128 is like shifting rigth 8 times
#echo $(($POWER_STATUS&amp;0x80))
echo "AC_STATUS="$AC_STATUS
# echo $AC_STATUS
</pre>
<strong>Example :</strong>

battery charging
<pre>rzbo@ubuntu:~$ ./battery_info.sh
BAT_STATUS=0
CHARG_IND=1
BAT_EXIST=1
CHARGE_CTL=0xd0
CHARGE_CTL2=0x47
Battery voltage = 3895.1mV
Battery discharge current = 304.0mA
Battery charge current = 0mA

rzbo@ubuntu:~$ ./power_status.sh
AC_STATUS=1</pre>
<strong>Battery discharging (USB power unplugged)</strong>
<pre>rzbo@ubuntu:~$ ./battery_info.sh
BAT_STATUS=0
CHARG_IND=0
BAT_EXIST=1
CHARGE_CTL=0xd0
CHARGE_CTL2=0x47
Battery voltage = 3678.4mV
Battery discharge current = 0mA
Battery charge current = 176.0mA

rzbo@ubuntu:~$ ./power_status.sh
AC_STATUS=0</pre>
<h2></h2>
<a href="http://dostmuhammad.com/wp-content/uploads/2015/06/IMG_20140916_183651.jpg"><img class="alignnone size-medium wp-image-3345" src="http://dostmuhammad.com/wp-content/uploads/2015/06/IMG_20140916_183651-300x168.jpg" alt="IMG_20140916_183651" /></a> <a href="http://dostmuhammad.com/wp-content/uploads/2015/06/IMG_20140916_183625.jpg"><img class="alignnone size-medium wp-image-3346" src="http://dostmuhammad.com/wp-content/uploads/2015/06/IMG_20140916_183625-225x300.jpg" alt="IMG_20140916_183625" /></a>