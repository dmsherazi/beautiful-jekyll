---
ID: 2869
post_title: 'How to play ringtone/alarm/notification  sound in Android'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/how-to-play-ringtonealarmnotification-sound-in-android/
published: true
post_date: 2015-01-04 07:32:32
---
Playing the default notification sound of the device is the most effective way to notify a user. This can be established by getting the Uri of the audio file from RingtoneManager. To play default alarm tone , ringtone or notification sound from an android app, the following code snippet is useful.
<h3>Play Notification Tone</h3>
<pre class="brush:cpp">try {
 Uri notification = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_NOTIFICATION);
 Ringtone r = RingtoneManager.getRingtone(getApplicationContext(), notification);
 r.play();
 } catch (Exception e) {
 e.printStackTrace();
 }</pre>
<h3>Play Alarm Tone</h3>
To play an Alarm-tone change TYPE_NOTIFICATION to TYPE_ALARM.
<pre class="brush:cpp">try {
 Uri notification = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_ALARM);
 Ringtone r = RingtoneManager.getRingtone(getApplicationContext(), notification);
 r.play();
 } catch (Exception e) {
 e.printStackTrace();
 }
</pre>
<h3>Set &amp; Play a Tone from Raw resources folder</h3>
To set a file from the raw folder of your app just change the uri to get the desired file from raw resources. If you have included a tone called sownd.mp3 in your raw resources folder, all you have to do is change
<pre class="brush:cpp"> Uri notification = RingtoneManager.getDefaultUri(RingtoneManager.TYPE_ALARM);</pre>
to
<pre>  Uri path = Uri.parse("android.resource://"+getPackageName()+"/raw/sound.mp3");</pre>
The code should look like this now
<pre class="brush:cpp">try {
  Uri path = Uri.parse("android.resource://"+getPackageName()+"/raw/sound.mp3");
  // The line below will set it as a default ring tone replace
  // RingtoneManager.TYPE_RINGTONE with RingtoneManager.TYPE_NOTIFICATION
  // to set it as a notification tone
  RingtoneManager.setActualDefaultRingtoneUri(
                    getApplicationContext(), RingtoneManager.TYPE_RINGTONE,
                    path);
  Ringtone r = RingtoneManager.getRingtone(getApplicationContext(), path); 
  r.play();
 } 
catch (Exception e) {
 e.printStackTrace(); 
}</pre>