---
ID: 2525
post_title: >
  Disable CLK Pre-scaler in AVR to use
  8MHz Internal Oscilator
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/disable-clk-pre-scaler-in-avr-to-use-8mhz-internal-oscilator/
published: true
post_date: 2014-04-12 07:27:46
---
Just wanted to share this small piece of information that can help many . If you want to Run your AVR at 8MHz from the internal oscillator you need to disable the CLK/8 Fuse. You can do this by burning new fuse values. This can also be done in you main function as well. Below is a piece of code that will change the pre-scaler to zero.
<pre>
// set the clock speed to "no pre-scaler" (8MHz with internal osc or
// full external speed)
// set the clock prescaler. First write CLKPCE to enable setting of clock the
// next four instructions.
CLKPR=(1< <clkpce); // change enable
CLKPR=0; // "no pre-scaler"
_delay_us(60); // 60us
</pre>
Hope this will help!</pre>