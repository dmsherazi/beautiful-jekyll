---
ID: 2631
post_title: Configuring Power Rails in Proteus ISIS
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/configuring-power-rails-in-proteus-isis/
published: true
post_date: 2014-04-24 19:43:11
---
Proteus ISIS is a nice and powerful simulation tool for electronic designs. For most ICs the supply pins are hidden and they are connected to the 5v power rail by default. Some times one need to use other than 5V value for the supply and i have seen many people don’t know how to do it. In this short post I would show how you can change the value but first if just want to connect the 5V supply to other devices.

In case you don’t want to change the supply voltage and just want to connect it to other devices its fairly simple. Follow the steps
<ul>
	<li>Select “Terminals mode” from the left toolbar</li>
	<li>from the terminals list you can select “Power” or “Ground” and place on the schematic. Power and ground are the power rails that are connected to the hidden pins</li>
	<li>That’s it, check the images bellow.</li>
</ul>
This is how it would appear on the schematic.

Changing the Power Rails Volatge

So if you want to use other than 5V power supply you can configure it from the “Design&gt;&gt;Configure Power rails” menu entry. Proteus would give you a dialogue box if you followed this menu from where you can change the value for VCC/VDD and VEE . Just type in the required value and hit OK.

that would lead to the final step.

cheers!