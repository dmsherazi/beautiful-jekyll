---
ID: 2373
post_title: >
  Show State if Sim900 originated call is
  recieved
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
published: true
post_date: 2013-12-14 14:22:46
---
By default when you make a voice call Sim900 doesn't send any response if the called party picks the call. Sometime its important to know if the other side is getting ring or has picked the call. In order to show the state we have to configure the module using the following AT Command <pre>AT+MORING=1</pre>
After sending the is command if a number is dialed, a URC string "MO RING" will be received if the other mobile is alerted and "MO CONNECTED" will be received if the call is answered.
