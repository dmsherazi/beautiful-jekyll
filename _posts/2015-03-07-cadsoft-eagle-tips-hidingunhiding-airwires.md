---
ID: 3070
post_title: '[Cadsoft Eagle tips] hiding/unhiding Airwires'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/cadsoft-eagle-tips-hidingunhiding-airwires/
published: true
post_date: 2015-03-07 13:28:42
---
You can hide airwires only on a per signal basis.  If you turn off the  airwires for ground and power suplies you should have a much cleaner screen. Instead of using ratsnest ! <em>signal_name</em>, you can use the info command on a signal (airwire or trace) in the board window and you will see a check box “Airwires hidden” for that signal in the popup “Properties” window. Click on it and all airwires for that signal will be gone.<span id="more-901"></span>

<strong>Hiding selected airwires</strong>
Sometimes it may be useful to hide the airwires of selected signals, for instance if these will later be connected through a polygon. Typically this could be supply signals, which have a lot of airwires that will never be routed explicitly and just obscure the other signals’ airwires.
To hide airwires the RATSNEST command can be given the exclamation mark (‘!’), followed by a list of signals, as in
<div>

<code class="cpp plain">RATSNEST ! GND VCC</code>

which would hide the airwires of the signals GND and VCC.
To have the airwires displayed again just enter the RATSNEST command without the ‘!’ character, and the list of signals:

<code class="cpp plain">RATSNEST GND VCC</code>

This will activate the display of the airwires of the signals GND and VCC and also recalculates them. You can also recalculate the airwires (and polygons) of particular signals this way.
The signal names may contain wildcards, and the two variants may be combined, as in

<code>RATSNEST D* ! ?GND VCC</code>

which would recalculate and display the airwires of all signals with names beginning with ‘D’, and hide the airwires of all the various GND signals (like AGND, DGND etc.) and the VCC signal. Note that the command is processed from left to right, so in case there is a DGND signal the example would first process it for display, but then hide its airwires.
To make sure all airwires are displayed enter

<code>RATSNEST *</code>

Use ‘RATS *’ at the command prompt to show all airwires.”

</div>