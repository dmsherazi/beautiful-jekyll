---
ID: 3436
post_title: >
  GET request using AT commands SIM800
  SIM900
author: Dost Muhammad Shah
post_excerpt: 'In this post I am writing how to send a GET request using GSM Module with AT commands. It should work with any module and has been tested to work with Sim800 series  (SIM800C-DS , SIM800A, SIM800H, SIM800L, SIM800C, SIM800 etc) and Sim900 series (SIM900, SIM900A, SIM900D, SIM900B) of modules from simcom.'
layout: post
permalink: >
  http://dostmuhammad.com/blog/making-get-request-using-at-commands-sim800-sim900/
published: true
post_date: 2015-12-15 07:34:57
---
In this post I am writing how to send a GET request using GSM Module with AT commands. It should work with any module and has been tested to work with Sim800 series  (<a href="http://simcomm2m.com/module/detail.aspx?id=132">SIM800C-DS</a> , <a href="http://simcomm2m.com/module/detail.aspx?id=129">SIM800A</a>, <a href="http://simcomm2m.com/En/module/detail.aspx?id=75">SIM800H</a>, <a href="http://simcomm2m.com/module/detail.aspx?id=13">SIM800L</a>, <a href="http://simcomm2m.com/En/module/detail.aspx?id=74">SIM800C</a>, <a href="http://simcomm2m.com/En/module/detail.aspx?id=138">SIM800 </a>etc) and Sim900 series (<a href="http://simcomm2m.com/En/module/detail.aspx?id=71">SIM900</a>, <a href="http://simcomm2m.com/module/detail.aspx?id=7">SIM900A</a>, <a href="http://simcomm2m.com/En/module/detail.aspx?id=73">SIM900D</a>, <a href="http://simcomm2m.com/En/module/detail.aspx?id=72">SIM900B</a>) of modules from simcom.

You have to bring up GPRS connection before this obviously , which is not covered here in this post.

&nbsp;
<h2>HERE ARE THE STEPS TO MAKE GET REQUEST</h2>
Initiate the HTTP service
<pre>AT+HTTPINIT
&gt; OK</pre>
Set the HTTP session.
<pre>AT+HTTPPARA=”CID”,1
&gt; OK</pre>
Set the HTPP URL
<pre>at+httppara=”URL”,”google.com”</pre>
Start the session&lt;
<pre>AT+HTTPACTION=0
&gt; OK

&gt; +HTTPACTION:0,601,0</pre>
The above AT response code<strong> (601)</strong> for HTTP session start indicates that there is a network error. Then make sure that the PDP context is setup properly.

IF the HTTP session is successful, it should return code of <strong>’200′</strong>,
<pre>AT+HTTPACTION=0
&gt; OK
&gt; +HTTPACTION:0,200,4</pre>
Above HTTP GET request is sucessful and it returned 4 bytes.
To read the data of the HTTP server,
<pre>AT+HTTPREAD
&gt; +HTTPREAD:4
&gt; test
&gt; OK</pre>
To terminate the HTTP service,
<pre>AT+HTTPTERM
&gt; OK
</pre>
<h3>UPDATE:</h3>
Sometimes a 601 Error code is received in response. @Bruno Lewin shared a link to a <a href="http://stackoverflow.com/questions/15975051/error-httpaction0-601-0" target="_blank">StackOverFlow Answer</a> about the issue and I feel that I should include it here as well
<blockquote>&nbsp;

Here are the minimum setup commands that have worked for me (based on trial/error and searching around on the internet).
<pre><code>AT+SAPBR=3,1,"APN","wap.cingular"
AT+SAPBR=1,1
</code></pre>
The correct value for the APN may be different for you, depending on your network and service provider.

Status codes above 600 (and some in the 500 range) are unassigned in the HTTP standard. In the AT command manual for the SIM908, status meanings are given in the notes on the <code>HTTPACTION</code>command:
<pre><code>600 Not HTTP PDU
601 Network Error
602 No memory
603 DNS Error
604 Stack Busy
</code></pre>
You can query the bearer connection status of CID 1 with <code>AT+SAPBR=2,1</code> and the related parameters with <code>AT+SAPBR=4,1</code>. You can also check that you're attached to the GPRS network with <code>AT+CGATT?</code>. If everything indicates that you are connected and you are still getting a 601 status code, then check that your service plan has data and that it hasn't run out. I have found that even when my account has a few hundred k of data showing on the balance that I start to get a 601 status until I add more data to my prepaid phone plan. If the SIM module has been on the whole time and you add more data, you'll need to close and re-open your connection (<code>AT+SAPBR=0,1</code> followed by <code>AT+SAPBR=1,1</code>) and then your <code>HTTP*</code> commands will start working again without having to set the <code>HTTPPARA</code> settings again and without having to restart with <code>HTTPINIT</code>.</blockquote>