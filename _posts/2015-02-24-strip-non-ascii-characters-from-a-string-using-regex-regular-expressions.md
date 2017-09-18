---
ID: 3091
post_title: >
  strip non-ASCII characters from a string
  using RegEx (Regular expressions)
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/strip-non-ascii-characters-from-a-string-using-regex-regular-expressions/
published: true
post_date: 2015-02-24 12:36:03
---
In case you have a string data which has some non ASCII characters and want to strip off all those non-ASCII characters the following regular expression will help you.
<pre class="lang:c++ highlight:0 decode:true ">[^u0000-u007F]+</pre>
Explanation
<ul>
	<li><span class="treeCharclass">[^u0000-u007F]+</span> match a single character not present in the list below
<div class="file"><span class="note">Quantifier:</span> <span class="inner-quantifier">+</span> Between <span class="quantifier">one</span> and <span class="quantifier">unlimited</span> times, as many times as possible</div></li>
	<li>
<div class="file"><span class="token">u0000-u007F</span> a single character in the range between the following two characters</div>
<ul style="font-weight: inherit;">
	<li>
<div class="file"><span class="token">u0000</span> the literal character <span class="literal">u0000</span> (case sensitive)</div></li>
	<li>
<div class="file"><span class="token">u007F</span> the literal character <span class="literal">u007F</span> (case sensitive)</div></li>
</ul>
</li>
</ul>
^ is the not operator. It tells the regex to find everything that doesn't match, instead of everything that does match.

The u####-u#### says which characters match.u0000-u007F is the equivilent of the first 255 characters in utf-8 or unicode, which are always the ASCII characters. So you match every non ASCII character (because of the not)

<!--more-->

I had a string like the one below where there are many non standard chars
<pre class="highlight:0">name 1= Chanel 51������������������������������������������������������������
</pre>
Applying the replace all method in java as below
<pre class="highlight:0"> String s=   "name 1= Chanel 51������������������������������������������������������������"
s = s.replaceAll("[^u0000-u007F]+","");
System.out.println(s);
</pre>
would output the following to console
<pre class="highlight:0">name 1= Chanel 51</pre>
Test it here<a href="http://dostmuhammad.com/blog/strip-non-ascii-characters-from-a-string-using-regex-regular-expressions/%20https://regex101.com/">https://regex101.com</a>

ASCII Table for reference.

<img src="http://www.asciitable.com/index/asciifull.gif" alt="Ascii Table" />

Extended ASCII characters

&nbsp;

<img src="http://www.asciitable.com/index/extend.gif" alt="EBCDIC and IBM Scan Codes" />