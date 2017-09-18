---
ID: 3464
post_title: >
  isOnline() check if android device has
  internet connectivity
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/isonline-check-android-device-internet-connectivity/
published: true
post_date: 2016-06-18 16:32:05
---
<h2>What do you want?</h2>
<ul>
 	<li>If you just want to check for a <strong>connection to any network</strong> - not caring if internet is available - then most of the answers here (including the accepted), implementing <code>isConnectedOrConnecting()</code> will work well.</li>
 	<li>If you want to know if you have an <strong>internet connection</strong> (as the question title indicates) please read on</li>
</ul>
<h2>Ping for the main name servers</h2>
<pre class="language-javascript">public boolean isOnline() {
    Runtime runtime = Runtime.getRuntime();
    try {
       Process ipProcess = runtime.exec("/system/bin/ping -c 1 8.8.8.8");
        int     exitValue = ipProcess.waitFor();
        return (exitValue == 0);
    } catch (IOException e)          { e.printStackTrace(); } 
      catch (InterruptedException e) { e.printStackTrace(); }
    return false;
}</pre>
That's it! Yes that short, yes it is fast, no it does not need to run in background, no you don't need root privileges.
<h2>Possible Questions</h2>
<ul>
 	<li><em>Is this really fast enough?</em>Yes, very fast!</li>
 	<li><em>Is there really no reliable way to check if internet is available, other than testing something on the internet?</em>Not as far as I know, but let me know, and I will edit my answer.</li>
 	<li><em>Couldn't I just ping my own page, which I want to request anyways?</em>Sure! You could even check both, if you want to differentiate between "internet connection available" and your own servers beeing reachable</li>
 	<li><em>What if the DNS is down?</em>Google DNS (e.g. <code>8.8.8.8</code>) is the largest public DNS service in the world. As of 2013 it serves 130 billion requests a day. Let 's just say, your app not responding would probably not be the talk of the day.</li>
 	<li><em>Which permissions are required?</em>
<pre>&lt;uses-permission android:name="android.permission.INTERNET" /&gt;</pre>
Just internet access - what surprise ^^ (BTW have you ever thought about, how some of the methods suggested here could even have a remote glue about the availability of internet, without this permission?)</li>
</ul>