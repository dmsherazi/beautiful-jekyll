---
ID: 3151
post_title: >
  SMASH / UNSMASH all parts or a grouped
  parts in Cadsoft EAGLE
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/smash-unsmash-all-parts-or-a-grouped-parts-in-cadsoft-eagle/
published: true
post_date: 2015-03-12 17:43:27
---
At times you require to SMASH or UNSMASH a number of components at a time either for rearranging the names or re size their text. Sometime you might need to UNSMASH them. This is important for making the sikscreens legible and look nice.

Although this is possible through the use of ULPs , here is how it can be implemented by command line of eagle.

For smashing  all parts/components , use the following command
<pre>GROUP ALL; SMASH (&gt;0 0);</pre>
For unsmashing  all parts/components , use the following command
<pre>GROUP ALL; SMASH (S&gt; 0 0);</pre>
For smashing  already grouped parts/components , use the following command
<pre>SMASH (&gt;0 0);</pre>
For unsmashing  already grouped parts/components , use the following command
<pre>SMASH (S&gt; 0 0);</pre>
Cheers :)