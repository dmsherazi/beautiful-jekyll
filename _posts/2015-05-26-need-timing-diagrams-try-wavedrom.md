---
ID: 3318
post_title: NEED TIMING DIAGRAMS? TRY WAVEDROM
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/need-timing-diagrams-try-wavedrom/
published: true
post_date: 2015-05-26 05:38:52
---
<header class="entry-header">
<div class="entry-featured-image"><img src="https://hackadaycom.files.wordpress.com/2015/05/wavedrom2.png?w=800" alt="" /></div>
</header>
<div class="entry-content">

When working with anything digital, you’re going to end up reading or writing a timing diagram before long. For us, that’s meant keeping (text) notes, drawing something on a napkin, or using a tool like Inkscape. None of these are ideal.

An afternoon’s search for a better tool ended up with <a href="http://wavedrom.com/" target="_blank">Wavedrom</a>.

Just so you know where we’re coming from, here’s our list of desiderata for a timing diagram drawing solution:
<ul>
	<li>Diagrams have a text-based representation, so their generation can be easily scripted and the results versioned and tracked throughout project development</li>
	<li>Command-line rendering of images, because we like to automate everything</li>
	<li>Looks good</li>
	<li>Simple to use for common cases, but flexible enough to do some strange stuff when needed</li>
	<li>Output modifiable when absolutely necessary: SVG would be nice</li>
</ul>
Basically, what we want is <a href="http://www.graphviz.org/" target="_blank">graphviz</a> for timing diagrams.

Wavedrom nails four out of these five at the moment, and has promise to cover all of the bases. Give the <a href="http://wavedrom.com/editor.html" target="_blank">online editor</a> demo a try. We found it intuitive enough that we could make simple diagrams without even reading the fine manual. The <a href="http://wavedrom.com/tutorial.html" target="_blank">tutorial</a> has got you covered for more esoteric use cases.

<a href="https://hackadaycom.files.wordpress.com/2015/05/foo.png" target="_blank"><img class=" size-medium wp-image-156807 alignright" src="https://hackadaycom.files.wordpress.com/2015/05/foo.png?w=400&amp;h=122" alt="foo" width="400" height="122" /></a>

Clearly, some good thought has been put into the waveform description language, <a href="https://github.com/drom/wavedrom/wiki/WaveJSON" target="_blank">WaveJSON</a>; it’s mostly readable and makes the essentials quick and easy. Because you can also enter straight SVG, it leaves the door open for full-fledged lunacy.

Wavedrom is written in JavaScript, and built for embedding in webpages; that’s the way they intend us to use it. On the other hand, if you want to run your own local version of the online editor, you can <a href="https://github.com/wavedrom/wavedrom.github.io/releases" target="_blank">download it</a> and install it locally if you’d like.

Our only quibble is that the standalone, command-line application wouldn’t generate images without the GUI on our Arch system. (Looks like there are some Google Chrome dependencies?) Otherwise, we think we’ve found our solution.

There are other applications out there. <a href="http://drawtiming.sourceforge.net/samples.html" target="_blank">Drawtiming</a> looks good, but we can’t quite get our head around the file format and the graphic output isn’t as flexible as we’d like: it only outputs GIF and we’re more into SVG because it can be edited easily after the fact.

There are font-based solutions that let you “type” the timing diagrams. We found <a href="http://www.josephpalmer.com/cgi-local/View_Permalink.cgi?entry=2004/6/30/02:31:40:163" target="_blank">Xwave</a> and “<a href="http://www.pcserviceselectronics.co.uk/fonts/index.php" target="_blank">Timing Diagram Font</a>“. These work but aren’t particularly flexible; if you want something to happen at odd times, you’re out of luck. Plus, it just feels like a dirty hack, as if that were a bad thing.

Latex users can use <a href="http://www.ctan.org/tex-archive/graphics/pgf/contrib/tikz-timing/" target="_blank">tikz-timing</a>, which makes sketching out your timing diagrams as much fun as laying out a very complex table in Latex (that is: not fun at all). On the other hand, it looks good, is ultimately flexible, outputs PDF, and would be scriptable if someone put the time in to write a nice frontend.

So for the next little while, we’re trying out Wavedrom.

What do you use for making timing diagrams?

VIA: <a href="http://hackaday.com/2015/05/25/need-timing-diagrams-try-wavedrom/">HACKADAY</a>

</div>