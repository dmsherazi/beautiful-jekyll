---
ID: 2610
post_title: >
  Disable PIN code using Gsm modem AT
  commands
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/disable-pin-code-using-gsm-modem-at-commands/
published: true
post_date: 2014-04-24 18:07:50
---
If you have a <strong>PIN code</strong> enabled SIM card and want to remove /disable PIN code using AT commands follow these commands,
suppose <strong>9546</strong> is the current PIN code , Replace 9546 with your PIN code, &gt;&gt;&gt; shows the response from modem.
<pre class="lang:default decode:true">AT+CPIN?
&gt;&gt;&gt; +CPIN: SIM PIN // pin codes need to be entered
&gt;&gt;&gt; OK

AT+CPIN="9546"
&gt;&gt;&gt;; OK

AT+CLCK="SC",0,"9546" // disable pin code
&gt;&gt;&gt; OK

AT+CPIN?
&gt;&gt;&gt; +CPIN: READY</pre>
&nbsp;