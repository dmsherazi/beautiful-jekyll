---
ID: 3231
post_title: >
  Solar Charge Controller Improves
  Efficiency of Solar Panels
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/solar-charge-controller-improves-efficiency-of-solar-panels/
published: true
post_date: 2015-03-20 14:32:01
---
The simplest and easiest way to charge a battery with a solar panel is to connect the panel directly to the battery. Assuming the panel has a diode to prevent energy from flowing through it from the battery when there’s no sunlight. This is fairly common but not very efficient. [Debasish Dutta] has built a charge controller that addresses the inefficiencies of such a system though, and was able to <a href="http://hackaday.io/project/4613-arduino-mppt-solar-charge-controller">implement maximum power point tracking using an Arduino</a>.

<a href="http://en.wikipedia.org/wiki/Maximum_power_point_tracking">Maximum power point tracking</a> (MPPT) is a method that uses PWM and a special DC-DC converter to match the impedance of the solar panel to the battery. This means that more energy can be harvested from the panel than would otherwise be available. The circuit is placed in between the panel and the battery and regulates the output voltage of the panel so it matches the voltage on the battery more closely. [Debasish] reports that an efficiency gain of 30-40% can be made with this particular design.

This device has a few bells and whistles as well, including the ability to log data over WiFi, an LCD display to report the status of the panel, battery, and controller, and can charge USB devices. This would be a great addition to any solar installation, especially if <a href="http://hackaday.com/2012/05/16/prototyping-a-solar-charger-for-your-truck/">you’ve built one into your truck</a>.

via <a href="http://hackaday.com/2015/03/17/solar-charge-controller-improves-efficiency-of-solar-panels/">Hackaday</a>