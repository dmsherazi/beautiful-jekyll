---
ID: 2541
post_title: “The IC Time Machine”
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/the-ic-time-machine/
published: true
post_date: 2014-04-12 10:07:27
---
<h5 style="color: #000000;"><em>What is it?</em></h5>
<p style="color: #000000;">“A highly stable controller capable of producing accurate time delays, or oscillation.”
-Philips Components and Semiconductors</p>
<p style="color: #000000;">The 555 is a 8-pin intergrated circuit with 2 modes of opperation. The time delay (stable) mode is controlled by one capacitor and one resistor. The oscillation (astable) mode is controlled by a capacitor and two resistors. There is also a third mode Bistable mode or Schmitt trigger  : the 555 can operate as a flip-flop, if the DIS pin is not connected and no capacitor is used. This post will focus on some of the basics of 555 ic.</p>
<p style="color: #000000;"><strong>Navigation</strong></p>
<p style="color: #000000;"><a href="#introduction">1. 555 ic introduction</a></p>
<p style="color: #000000;"><a href="#pc">2. Pin configuration</a></p>
<p style="color: #000000;"><a href="#OM">3. Operation modes</a></p>
<p style="color: #000000;"><a href="#CS">4. Component  selection</a></p>
<p style="color: #000000;"><a href="#SP">5. Specifications for NE555</a></p>
<p style="color: #000000;"><a href="#dr">6. Derivatives</a></p>
<p style="color: #000000;"><a href="#rs">7. Resources</a></p>
<!--more-->
<h5 style="color: #000000;"><a id="introduction"></a>1. 555 ic introduction</h5>
<p style="color: #000000;"><a href="#nav">top</a>
Around 1971, the Signetics Corporation introduced the 555 timer IC. It was called “The IC Time Machine”. It was also the first and only commercial IC timer available at the time.</p>
<p style="color: #000000;">he 555 Integrated Circuit (IC) is an easy to use timer that has many applications. It is widely used in electronic circuits and this popularity means it is also very cheap to purchase. A ‘dual’ version called the 556 is also available which includes two independent 555 ICs in one package.</p>
<p style="color: #000000;"><img src="http://i1.wp.com/www.semiconductormuseum.com/Transistors/LectureHall/Camenzind/Camenzind_Page2_files/image002.gif?resize=313%2C268" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">This IC is a  monolithic timing circuit that can produce accurate and highly stable time delays or oscillation. Like other commonly used op-amps, this IC is also very much reliable, easy to use and cheaper in cost. It has a variety of applications including monostable and astable multivibrators, dc-dc converters, digital logic probes, waveform generators, analog frequency meters and tachometers, temperature measurement and control devices, voltage regulators etc. The timer basically operates in one of the two modes either as a monostable (one-shot) multivibrator or as an astable (free-running) multivibrator.The SE 555 is designed for the operating temperature range from – 55°C to 125° while the NE 555 operates over a temperature range of 0° to 70°C.</p>

<h5 style="color: #000000;"><a id="pc"></a>2. Pin Configuration</h5>
<p style="color: #000000;"><a href="#nav">top</a>
The following illustration shows  the 555 (8-pin).</p>
<p style="color: #000000;"><img src="http://i2.wp.com/upload.wikimedia.org/wikipedia/commons/thumb/c/c7/555_Pinout.svg/220px-555_Pinout.svg.png" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">In a circuit diagram the 555 timer chip is often drawn with pins not in the same order as the actual chip, this is because it is much easier to recognize the function of each pin, and makes drawing circuit diagrams much easier.</p>
<p style="color: #000000;">Pin functions:</p>
<p style="color: #000000;"><strong><em>Trigger input:</em></strong> when less than 1/3 Vs (‘active low’) this makes the output high (+Vs). It monitors the discharging of the timing capacitor in an astable circuit. It has high input impedance greater than 2M.</p>
<p style="color: #000000;"><strong><em>Threshold input</em></strong><strong>: </strong>when greater than 2/3 Vs (‘active high’) this makes the output low (0V)*. It monitors the charging of the timing capacitor in astable and monostable circuits. It has high input impedance greater than 10M.
* <em>providing the trigger input is &gt; 1/3 Vs, otherwise the trigger input will override the threshold input and hold the output high (+Vs).</em></p>
<p style="color: #000000;"><strong><em>Reset input</em></strong><strong>:</strong> when less than about 0.7V (‘active low’) this makes the output low (0V), overriding other inputs. When not required it should be connected to +Vs. It has an input impedance of about 10k.</p>
<p style="color: #000000;"><strong><em>Control input</em></strong>: this can be used to adjust the threshold voltage which is set internally to be 2/3Vs, usually this function is not required and the control input is connected to 0V with a 0.01µF capacitor to eliminate electrical noise. It can be left unconnected if noise is not a problem.</p>
<p style="color: #000000;"><strong><em>Discharge pin</em></strong> it is connected to 0V when the timer output is low and is used to discharge the timing capacitor in astable and monostable circuits.</p>
<p style="color: #000000;"><strong><em>Output pin </em></strong>of a standard 555 or 556 can sink and source up to 200mA. This is more than most ICs and is sufficient for many output transducers, including LEDs (with a resistor in series), low current lamps, piezo transducers, loudspeakers, relay coils and some motors. The output voltage does not quite reach 0V and +Vs, especially if a large current is flowing. To switch larger currents a transistor is needed to be used as switch.</p>

<h5 style="color: #000000;"><strong><em>
</em></strong><strong><em>3.  Operational modes</em></strong></h5>
<p style="color: #000000;"><a href="#nav">top</a>
The 555 timer has  following  operational modes</p>

<ul>
	<li>Monostable mode: in this mode, the 555 functions as a “one-shot”. Applications include timers, missing pulse detection, bouncefree switches, touch switches, frequency divider, capacitance measurement, pulse-width modulation (PWM) etc</li>
	<li>Astable – free running mode: the 555 can operate as an oscillator. Uses include LED and lamp flashers, pulse generation, logic clocks, tone generation, security alarms, pulse position modulation, etc.</li>
	<li>Bistable mode or Schmitt trigger: the 555 can operate as a flip-flop, if the DIS pin is not connected and no capacitor is used. Uses include bouncefree latched switches, etc.</li>
</ul>
<h6 style="color: #000000;"><strong>One shot, monostable:</strong>
<a href="#nav">top</a></h6>
<p style="color: #000000;">In the one-shot mode, the 555 acts like a monostable multivibrator. A monostable is said to have a single stable state–that is the off state. Whenever it is triggered by an input pulse, the monostable switches to its temporary state. It remains in that state for a period of time determined by an RC network. It then returns to its stable state. In other words, the monostable circuit generates a single pulse of fixed time duration each time it receives and input trigger pulse. Thus the name one-shot. One-shot multivibrators are used for turning some circuit or external component on or off for a specific length of time. It is also used to generate delays. When multiple one-shots are cascaded, a variety of sequential timing pulses can be generated. Those pulses will allow you to time and sequence a number of related operations.</p>
<p style="color: #000000;">The width of the output pulse is determined by the time constant of an RC network, which consists of a capacitor (C) and a resistor (R). The output pulse ends when the charge on the C equals 2/3 of the supply voltage. The output pulse width can be lengthened or shortened to the need of the specific application by adjusting the values of R and C.</p>
<p style="color: #000000;">The output pulse width of time <em>t</em>, which is the time it takes to charge C to 2/3 of the supply voltage, is given by</p>

<dl style="color: #000000;"><dd><img src="http://i2.wp.com/www.doctronics.co.uk/Images_gif/eq_555_17.gif" alt="monostable design equation" data-recalc-dims="1" /></dd></dl>
<p style="color: #000000;">where t is in seconds, R is in ohms and C is in farads.</p>
<p style="color: #000000;">The circuit used to make a 555 timer monostable is quite simple it just needs a few components.</p>
<p style="color: #000000;"><img src="http://i1.wp.com/upload.wikimedia.org/wikipedia/commons/thumb/1/19/555_Monostable.svg/220px-555_Monostable.svg.png" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">Now this is the basic circuit! u can build hundreds of modified monostables to add features and achieve different functions. We will add a few in to the blog soon.</p>

<h6 style="color: #000000;"><a id="as"></a><strong>Astable oscillator:</strong>
<a href="#nav">top</a></h6>
<p style="color: #000000;">In astable mode, the 555 timer puts out a continuous stream of rectangular pulses having a specified frequency. Resistor R<sub>1</sub> is connected between V<sub>CC</sub> and the discharge pin (pin 7) and another resistor (R<sub>2</sub>) is connected between the discharge pin (pin 7), and the trigger (pin 2) and threshold (pin 6) pins that share a common node. Hence the capacitor is charged through R<sub>1</sub> and R<sub>2</sub>, and discharged only through R<sub>2</sub>, since pin 7 has low impedance to ground during output low intervals of the cycle, therefore discharging the capacitor.</p>
<p style="color: #000000;">In the astable mode, the frequency of the pulse stream depends on the values of R<sub>1</sub>, VR<sub>1</sub> and C1: VR1 is made variable here so that we can adjust it to get variable time-period, for fixed time-period a fix value resistor should be used.The <a href="#CS">component selection program</a> can be used to get the values.</p>
<p style="color: #000000;"><a href="http://www.dostmuhammad.com/wp-content/uploads/2011/05/Untitled51.png"><img class="alignnone size-full wp-image-2155" title="Untitled5[1]" src="http://i0.wp.com/www.dostmuhammad.com/wp-content/uploads/2011/05/Untitled51.png?resize=381%2C600" alt="" data-recalc-dims="1" /></a></p>
<p style="color: #000000;">In astable mode the frequency cn be calculated as</p>
<p style="color: #000000;"><img src="http://i1.wp.com/www.doctronics.co.uk/Images_gif/eq_555_01.gif" alt="astable design formula" data-recalc-dims="1" /></p>
<p style="color: #000000;">The period, <em>t</em>, of the pulses is given by:</p>
<p style="color: #000000;"><img src="http://i2.wp.com/www.doctronics.co.uk/Images_gif/eq_555_05.gif?resize=248%2C66" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">The HIGH and LOW times of each pulse can be calculated from:</p>
<p style="color: #000000;"><img src="http://i1.wp.com/www.doctronics.co.uk/Images_gif/eq_555_02.gif?resize=278%2C42" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;"><img src="http://i0.wp.com/www.doctronics.co.uk/Images_gif/eq_555_03.gif?resize=230%2C42" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">The duty cycle of the waveform, usually expressed as a percentage, is given by:</p>
<p style="color: #000000;"><img src="http://i1.wp.com/www.doctronics.co.uk/Images_gif/eq_555_04.gif?resize=257%2C66" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">An alternative measurement of HIGH and LOW times is the mark space ratio:</p>
<p style="color: #000000;"><img src="http://i1.wp.com/www.doctronics.co.uk/Images_gif/eq_555_06.gif?resize=253%2C62" alt="" data-recalc-dims="1" /></p>
<p style="color: #000000;">It is usual to make <em>R</em>1=1 kΩ because this helps to give the output pulses a duty cycle close to 50%, that is, the HIGH and LOW times of the pulses are approximately equal.</p>

<h6 style="color: #000000;"><a id="bs"></a>Bistable Mode:</h6>
<p style="color: #000000;"><a href="#nav">top</a></p>
<p style="color: #000000;">In bistable mode, the 555 timer acts as a basic flip-flop. The trigger and reset inputs (pins 2 and 4 respectively on a 555) are held high via Pull-up resistors while the threshold input (pin 6) is simply grounded. Thus configured, pulling the trigger momentarily to ground acts as a ‘set’ and transitions the output pin (pin 3) to Vcc (high state). Pulling the reset input to ground acts as a ‘reset’ and transitions the output pin to ground (low state). No capacitors are required in a bistable configuration. Pins 5 and 7 (control and discharge) are left floating.</p>

<h5 style="color: #000000;"><em>4. Component selection</em></h5>
<p style="color: #000000;"><a href="#nav">top</a>
With a little practice, it is quite easy to choose appropriate values for a 555 timer astable. To make things even easier, you might like to download the <a href="http://www.doctronics.co.uk/programs/ic_555.exe">DOCTRONICS 555 timer component selection program</a> from DOCTRONICS.</p>
<p style="color: #000000;">The program works with all versions of Windows™ from Windows 95™ through to Windows 7™ and looks like this:</p>
<p style="color: #000000;"><a href="http://www.doctronics.co.uk/programs/ic_555.exe"><img src="http://i1.wp.com/www.doctronics.co.uk/images/555_03.gif?resize=446%2C347" alt="555 component selector" data-recalc-dims="1" /></a></p>
<p style="color: #000000;">To download the program, (~210K) click on the image. for detailed instructions on how to use click <strong><a href="http://www.doctronics.co.uk/down555.htm">here</a></strong></p>
<p style="color: #000000;">A online utility is also available  <a href="http://freespace.virgin.net/matt.waite/resource/handy/pinouts/555/">Online component selector</a></p>

<div style="color: #000000;">

<a id="SP"></a><strong>5. Specifications</strong>

<a href="#nav">top</a>

</div>
<p style="color: #000000;">These specifications apply to the NE555. Other 555 timers can have different specifications depending on the grade (military, medical, etc).</p>

<table style="color: #000000;">
<tbody>
<tr>
<td>Supply voltage (VCC)</td>
<td>4.5 to 15 V</td>
</tr>
<tr>
<td>Supply current (VCC = +5 V)</td>
<td>3 to 6 mA</td>
</tr>
<tr>
<td>Supply current (VCC = +15 V)</td>
<td>10 to 15 mA</td>
</tr>
<tr>
<td>Output current (maximum)</td>
<td>200 mA</td>
</tr>
<tr>
<td>Maximum Power dissipation</td>
<td>600 mW</td>
</tr>
<tr>
<td>Power Consumption (minimum operating)</td>
<td>30 mW@5V, 225 mW@15V</td>
</tr>
<tr>
<td>Operating temperature</td>
<td>0 to 70 °C</td>
</tr>
</tbody>
</table>
<h5 style="color: #000000;">6. <a id="dr"></a>Derivatives</h5>
<p style="color: #000000;"><a href="#nav">top</a></p>
<p style="color: #000000;">Many pin-compatible variants, including <a title="CMOS" href="http://en.wikipedia.org/wiki/CMOS">CMOS</a> versions, have been built by various companies. Bigger packages also exist with two or four timers on the same chip. The 555 is also known under the following type numbers:</p>

<table style="color: #000000;">
<tbody>
<tr>
<th>Manufacturer</th>
<th>Model</th>
<th>Remark</th>
</tr>
<tr>
<td>Avago Technologies</td>
<td>Av-555M</td>
<td></td>
</tr>
<tr>
<td>Custom Silicon Solutions</td>
<td>CSS555/CSS555C</td>
<td>CMOS from 1.2 V, IDD &lt; 5 µA</td>
</tr>
<tr>
<td>CEMI</td>
<td>ULY7855</td>
<td></td>
</tr>
<tr>
<td>ECG Philips</td>
<td>ECG955M</td>
<td></td>
</tr>
<tr>
<td>Exar</td>
<td>XR-555</td>
<td></td>
</tr>
<tr>
<td>Fairchild Semiconductor</td>
<td>NE555/KA555</td>
<td></td>
</tr>
<tr>
<td>Harris</td>
<td>HA555</td>
<td></td>
</tr>
<tr>
<td>IK Semicon</td>
<td>ILC555</td>
<td>CMOS from 2 V</td>
</tr>
<tr>
<td>Intersil</td>
<td>SE555/NE555</td>
<td></td>
</tr>
<tr>
<td>Intersil</td>
<td>ICM7555</td>
<td>CMOS</td>
</tr>
<tr>
<td>Lithic Systems</td>
<td>LC555</td>
<td></td>
</tr>
<tr>
<td>Maxim</td>
<td>ICM7555</td>
<td>CMOS from 2 V</td>
</tr>
<tr>
<td>Motorola</td>
<td>MC1455/MC1555</td>
<td></td>
</tr>
<tr>
<td>National Semiconductor</td>
<td>LM1455/LM555/LM555C</td>
<td></td>
</tr>
<tr>
<td>National Semiconductor</td>
<td>LMC555</td>
<td>CMOS from 1.5 V</td>
</tr>
<tr>
<td>NTE Sylvania</td>
<td>NTE955M</td>
<td></td>
</tr>
<tr>
<td>Raytheon</td>
<td>RM555/RC555</td>
<td></td>
</tr>
<tr>
<td>RCA</td>
<td>CA555/CA555C</td>
<td></td>
</tr>
<tr>
<td>STMicroelectronics</td>
<td>NE555N/ K3T647</td>
<td></td>
</tr>
<tr>
<td>Texas Instruments</td>
<td>SN52555/SN72555</td>
<td></td>
</tr>
<tr>
<td>Texas Instruments</td>
<td>TLC555</td>
<td>CMOS from 2 V</td>
</tr>
<tr>
<td>USSR</td>
<td>K1006ВИ1</td>
<td></td>
</tr>
<tr>
<td>Zetex</td>
<td>ZSCT1555</td>
<td>down to 0.9 V</td>
</tr>
<tr>
<td>NXP Semiconductors</td>
<td>ICM7555</td>
<td>CMOS</td>
</tr>
<tr>
<td>HFO / East Germany</td>
<td>B555</td>
<td></td>
</tr>
</tbody>
</table>
<h5 style="color: #000000;"><strong>7. <a id="rs"></a>RESOURCES:</strong></h5>
<p style="color: #000000;"><a href="#nav">top</a></p>
<p style="color: #000000;">DATASHEET:    <a href="http://www.fairchildsemi.com/ds/LM/LM555.pdf" target="_blank">555 data sheet</a></p>
<p style="color: #000000;"><a href="http://www.doctronics.co.uk/555.htm">555 timer</a> ( Doctronics.com)</p>
<p style="color: #000000;"><a href="http://www.sentex.ca/~mec1995/gadgets/555/555.html">555 Timer Tutorial</a> (Tony van Roon, University of Guelph, Canada)</p>
<p style="color: #000000;"><a href="http://en.wikipedia.org/wiki/555_timer_IC">555 timer IC</a> (from <em>Wikipedia</em>, the free encyclopaedia)</p>
<p style="color: #000000;"><a href="http://www.talkingelectronics.com/te_interactive_index.html">The 555 IC</a></p>
<p style="color: #000000;"><a href="http://freespace.virgin.net/matt.waite/resource/handy/pinouts/555/">Online component selector</a></p>