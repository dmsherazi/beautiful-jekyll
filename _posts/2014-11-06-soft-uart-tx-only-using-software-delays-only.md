---
ID: 2852
post_title: >
  Soft-Uart Tx only using software delays
  only
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/soft-uart-tx-only-using-software-delays-only/
published: true
post_date: 2014-11-06 07:27:31
---
I was working on a code for a module on my GSM gateway today , for which I had given 1 pin of micro-controller to use as software Tx. Software UARTs usually uses timers to make them robust, but I had already used them all. So I decided to write a code using software delays.

The UART logic is inverted , so to send logic 1 you have to send low signal  and vice versa . Here is my code , hope it might help someone else.

<pre class="brush:cpp">/*
* soft-uart Tx only without any timmer uses software delays
* the baud rate depends on the delay in us , here I am using
* 4800 with a 1 start bit, 8 databits and 1 stop bit
* if you wanna change the baud rate calculate it by 1/baud and
* modify the _delay_us();
*
* Created: 11/21/2012 1:52:37 PM
* Author: AbuUmar
*/
#include &lt;avr/io.h&gt;
#include &lt;util/delay.h&gt;
#define portlow PORTC&amp;=~0x01
#define porthigh PORTC|=0x01
void putchar_soft(char data_soft)
{
 char bit_count=10; // 1+8+1SB
 data_soft=~data_soft;
 char secc=1;char0:
 if (secc=1)
 portlow;
 else
 porthigh;
 _delay_us(208);
 //_delay_us(208);
 for ( char i = 0; i &lt; 8; i++ ) {
 if(data_soft &amp; 1)
 portlow;
 else
 porthigh;
 data_soft=data_soft&gt;&gt;1;
 _delay_us(208);
 }
 porthigh;
 _delay_us(208);
 _delay_us(208);
 return;
}
int main(void)
{
 DDRC|=0b00000001;
 porthigh;
char inte=0;
while(1)
 {
 // example use, initializing a var to 0 and sending the data
 // with 1 sec delays
 putchar_soft(inte) ;
 _delay_ms(250);
 _delay_ms(250);
 _delay_ms(250);
 _delay_ms(250);
 inte++;
 }
}</pre>