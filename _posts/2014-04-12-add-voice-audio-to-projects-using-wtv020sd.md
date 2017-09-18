---
ID: 2521
post_title: >
  Add Voice /Audio to projects using
  WTV020SD
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/add-voice-audio-to-projects-using-wtv020sd/
published: true
post_date: 2014-04-12 07:13:06
---
Adding sound to your projects is great, there can be several methods to do it. In this post i will show how we can use <a href="http://www.waytronic.com/voicemodule_show.asp?/12.html">wtv020-sd</a> module to get this task done. I wont go in detailed description of the module and will keep the post short and to the point. The module can be operated in a number of modes including pushbutton modes but the one we are going for is the 3 wire serial mode. its actually SDA,SCL and reset wires that we use. The module would play back the ad4 files stored on uSD Card. and spk+ and spk- pins can be connected directly to a speaker. More details about the module can be found in the datasheet and the webpage link.

The interface is simple. you only need to connect Supply , DI ,CLK and reset Pins to get it working although you may also connect some other pins also but this is what is really needed to get the module working.

<img src="http://dostmuhammad.com/wp-content/uploads/1.jpg" alt="connections" /><!--more-->


The timing diagrams in the datasheet can be used to write the program. I will share the code I use for this module.
below is the code .
<pre>#include <avr /io.h>

#define SCL 4                 //serial clock
#define SDA 5                 //serial data
#define RST 3                 //audio module reset
/*=============================Delay functions starts==========================*/
void delayus(unsigned int usec)  // Function to provide time delay in us.
{
  int i,j;
  for(i=0;i<usec ;i++)
  for(j=0;j&lt;2;j++);
}
void delayms(unsigned int msec)  // Function to provide time delay in msec.
{
  int i,j ;
  for(i=0;i<msec;i++)
  for(j=0;j&lt;2125;j++);
}

void delays(unsigned int sec)  // Function to provide time delay in sec.
{
  int i;
  for(i=0;i<msec;i++)
  delayms(1000);
}
/*=============================Delay functions Ends===========================*/
void send_audio(unsigned int value)
{
  unsigned int mask;
  PORTC|=(1<<scl);//=1;   delayms(2);   for (mask = 0x8000; mask > 0; mask >>= 1)
  {
    if (value & mask) PORTC|=(1< <sda);
    else              PORTC&=~(1<<sda);
    PORTC&=~(1<<scl);
    delayus(200);
    PORTC|=(1<<scl);
    delayus(200);
  }
  delayms(2);   //stop bit indication
}
void init_audio()
{
  PORTC|=(1<<scl);
  PORTC&=~(1<<sda);
  //Reseting the module
  PORTC|=(1<<rst);
  delayms(100);
  PORTC&=~(1<<rst);
  delayms(10);
  PORTC|=(1<<rst);
  delayms(300);

  send_audio(0xfff7);         // to set to maximum sound
}
</pre>
Here is an example code to play file 0005.ad4 for 5 secs and then stops the file and start playing file 0001.ad4.


<pre>main()
{
  DDRC=0b00011100;
  init_audio();
  send_audio(0005);
  delays(5);
        send_audio(0xFFFF); //stop playing
  send_audio(0001);
  while(1);

}</pre>
To convert your audio files to AD4 format you can use the tool provided by waytronics. Get the converter and Sample files from the zip file HERE</usec></avr></pre>