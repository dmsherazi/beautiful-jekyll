---
ID: 2528
post_title: 'Keeping track of time in embedded applications: millis();'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/keeping-track-of-time-in-embedded-applications-millis/
published: true
post_date: 2014-04-12 07:32:53
---
Its very handy to keep track of time in embedded programs. In this post I will implement a function called <strong>millis() </strong>which can be used to track time.  Arduino users will be familiar with this one. I would be doing it for AVR MCUs you can easily port it for others. this function returns the number of milliseconds since the MCU began running the current program. This number will overflow (go back to zero), after approximately 50 days.
It uses a hardware timer , in this post i will use timer0 . The first step is to initialize timer0 and interupts. lets start.
<pre>void timer0(){
  // To set clock:
  // 1MHZ is 1,000,000 ticks per second
  // 1000 milli in 1 second
  // xMHZ = 1000millis
  // so MHZ/millis gives # HZ per millis
  // (HZ/millis)/prescaler= Top counter number

  // EG:for 8MHZ clock
  // 8000000/1000
  // 8000.0000000000
  // 8000/256
  // 31.2500000000 TOP counter

  //set CTC (clear timer on compare match mode)
  TCCR0A = (1&lt; &lt;WGM01);
  //sets prescaler clkIO/256  ***THIS MIGHT CAUSE ISSUES SETS FOR ALL CLOCKS**!!!!
  TCCR0B = (1&lt;&lt;CS02);
  //sets interrupt enable for OCF0A (TIMER_COMPA_vect)
  TIMSK0 = (1&lt;&lt;OCIE0A);
  //sets TOP counter match A at 31
  OCR0A = 31;
}


volatile uint32_t millis()
{
 uint32_t mill;
 uint8_t oldSREG = SREG;
 // remember last value of interrupts
 // disable interrupts while we read timer0_millis or we might get an
 // inconsistent value (e.g. in the middle of a write to timer0_millis)
 cli();
 mill = millis_count;
 SREG = oldSREG; // rewrite reg value to turn back on interrupts
 return mill;
}</pre>
In the code shown above we have initialized timer/counter 0 to make an interrupt after every millisecond. Next we have to update our millisecond count.
<pre>//interrupt declaration
ISR(TIMER0_COMPA_vect)
{
  ++millis_count;
  //OCR0A = 10; //sets upper breakpoint A
}
</pre>
That’s it. Lets see how to use it! First we copy the current value in milis() to a variable.
<pre>uint32_t starttime=millis();
</pre>
and later we compare the new values with the start value. Here’s an example of a 25 second.
<pre>if(millis()-starttime &gt; 25000)
{
  // some code here
}</pre>
Note that the parameter for millis() is an unsigned long, errors may be generated if a programmer tries to do math with other datatypes such as ints.

There are a number of ways you can use this. Hope this post will help you