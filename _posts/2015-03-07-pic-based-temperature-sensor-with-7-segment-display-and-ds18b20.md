---
ID: 3054
post_title: >
  Pic based temperature sensor with 7
  segment display and ds18b20
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/pic-based-temperature-sensor-with-7-segment-display-and-ds18b20/
published: true
post_date: 2015-03-07 13:43:13
---
This circuit is a Digital Temerature Sensor using a Dallas '1-wire' DS18B20 Digital Thermometer

http://www.youtube.com/watch?v=BgGgik1DgQs
Firstly I would like to thank Pommie and Mike, K8LH from the Electro Tech Online Forum for their genourous help. This has been the most challenging project to date and they have helped immensely. They have tought me many valuable lessons about programming in Assembly language and it has really assitsted me in getting this project up and running.

Note: I would like to make a point that some snippets of their own code is used in this program. I have used it with their permission and please observe any copyrights or name recognition placed in the code. If you wish to use their snippets of code, please contact them via the Electro-Tech-Online forum.

<b>How It Works</b>

The DS18B20 is a direct-to-digital temperature sensor using Maxim's exclusive 1-Wire bus protocol that implements bus communication using one control signal. In regards to hardware, this particular sensor is particularly easy to interface to. It only requires 1 external pull-up resistor to operate as opposed to an analogue sensor which possibly needs multiple external components such as resistors and op-amps.

In regards to software, opposed to analogue sensors, the Dallas 1-wire digital sensors are arguably as easy to interface to. While an analogue sensor will need an Analogue to Digital conversion using a voltage reference and possibly using an op-amp, the Dallas 1-wire direct to digital sensors require precise timing when it comes to communication. This program is fairly basic in principle as all it does is obtain temperature data from the DS18B20 sensor and display the temperature in Degrees Celsius on a 4 digit, 7 segment display. But when it comes to actually doing this, as you will see from the .ASM file, it is more complicated than it sounds. In words; the program first initialises the PIC16F628A Microcontroller. It assigns the Inputs and Outputs, zero's all bank 0 RAM, initialises the display column select bit and configures TIMER 2. TIMER 2 is used to interrupt the normal loop of the program to update the 7 segment LED display.

After the Microcontroller has been setup, it begins communication with the DS18B20 Temperature Sensor. Communication routines take up just under half of the program memory. After the temperature has been gathered and stored in RAM, the Microcontroller takes the 12-bit signed/fraction integer and converts it into a decimal number then stores it in four general purpose registers in RAM.

For example, take the number D'95.8'. It is stored like this:
<div class="bbCodeBlock bbCodeCode">
<pre class="code">HUNS register = 0
TENS register = 9
ONES register = 5
TENTHS register = 8</pre>
</div>
These registers are then used within the Interrupt Service Routine to call a table to obtain display data.
The program runs continuously, updating the temperature on the display just over once per 1 second.

Features Summary:
<ul>
	<li>Temperature data gathered more than once per second.</li>
	<li>TIMER 2 interrupt driven display.</li>
	<li>Program expandable to include multiple sensors on the same 1-Wire bus.</li>
	<li>Temperature range of -55.0 - 127.9 Degrees Celsius.</li>
</ul>
Please see the DS18B20 Datasheet for detailed information on the device.

<img class="aligncenter size-medium wp-image-3191" src="http://dostmuhammad.com/wp-content/uploads/schematic-300x185.jpg" alt="schematic" /><img class="aligncenter size-medium wp-image-3192" src="http://dostmuhammad.com/wp-content/uploads/breadboard-300x225.jpg" alt="breadboard" />

&nbsp;

&nbsp;

<a href="http://dostmuhammad.com/wp-content/uploads/digitaltemperaturesensorbasic.zip">digitaltemperaturesensorbasic</a>.zip

Here is the <a href="http://www.electro-tech-online.com/content/409-digital-temerature-sensor.html">complete project</a>   (with explanation , code, schematic and video)
<h2></h2>