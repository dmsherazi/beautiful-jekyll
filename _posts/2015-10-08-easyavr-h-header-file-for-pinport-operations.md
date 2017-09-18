---
ID: 3394
post_title: 'easyavr.h  Header file for pin/port operations'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/easyavr-h-header-file-for-pinport-operations/
published: true
post_date: 2015-10-08 09:12:15
---
Here I am sharing a header file called <strong>easyavr.h</strong>. This is a pretty basic header file with some helper functions related to input output pins of AVR


<pre>#ifndef __EASYAVR_H_
#define __EASYAVR_H_


//  Sets pin of port to 1
//
//  Example for PD2: PIN_ON(PORTD, 2)
#define PIN_ON(port,pin) ((port) |= (1 &lt;&lt; (pin)))


//  Sets pin of port to 0
//
//  Example for PD2: PIN_OFF(PORTD, 2)
#define PIN_OFF(port,pin) ((port) &amp;= ~(1 &lt;&lt; (pin)))


//  Sets pin of port to value
//
//  Example for PD2: PIN_SET(PORTD, 2, 1)
#define PIN_SET(port,pin,val) (((val) &gt; 0) ? PIN_ON((port),(pin)) : PIN_OFF((port),(pin)))

//  Sets all of port pins to OUTPUT mode
//
//  Example for PORTD: PORT_AS_OUTPUT(PORTD)
#define PORT_AS_OUTPUT(port) ((port) = 0xFF)

//  Sets all of port pins to INPUT mode
//
//  Example for PORTD: PORT_AS_INPUT(PORTD)
#define PORT_AS_INPUT(port) ((port) = 0x00)

//  Sets pin of port to OUTPUT mode
//
//  Example for PD1: PORT_AS_OUTPUT(DDRD, 1)
#define PIN_AS_OUTPUT(ddr,pin) ((ddr) |= (1 &lt;&lt; (pin)))


//  Sets pin of port to INPUT mode
//
//  Example for PD1: PORT_AS_INPUT(DDRD, 1)
#define PIN_AS_INPUT(ddr,pin) ((ddr) &amp;= ~(1 &lt;&lt; (pin)))

//  Checks pin's value of port
//  Returns 1 or 0
//
//  Example for PD2: CHECK_PIN(PIND, 2)
#define CHECK_PIN(pinreg,pin) (((pinreg) &amp; (1 &lt;&lt; (pin))) != 0)


#endif</pre>