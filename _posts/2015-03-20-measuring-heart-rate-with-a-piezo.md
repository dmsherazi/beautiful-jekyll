---
ID: 3228
post_title: Measuring Heart Rate With A Piezo
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/measuring-heart-rate-with-a-piezo/
published: true
post_date: 2015-03-20 14:23:52
---
Look around for heart rate sensors that interface easily to microcontrollers, and you’ll come up with a few projects that use LEDs and <em>other </em>microcontrollers to do the dirty work of filtering out pulses in a wash of light.

[Thomas] was working on a project that detects if water is flowing through a pipe with a few piezoelectric sensors. Out of curiosity, he taped the sensor to his finger, and to everyone’s surprise, the values his microcontroller were spitting out <a href="http://www.ohnitsch.net/2015/03/18/measuring-heart-rate-with-a-piezoelectric-vibration-sensor/">were an extremely noise-free version of his heart rate</a>.

The piezo in question <a href="http://www.dfrobot.com/index.php?route=product/product&amp;product_id=399">is a standard, off the shelf module</a>, and adding this to a microcontroller is as easy as putting the piezo on an analog pin. From there, it’s just averaging measurements and extracting a heartbeat from the data.

Via <a href="http://hackaday.com/2015/03/19/measuring-heart-rate-with-a-piezo/">hackaday.com</a>