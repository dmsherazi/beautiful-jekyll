---
ID: 2634
post_title: How to filter logcat in Android Studio?
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/how-to-filter-logcat-in-android-studio/
published: true
post_date: 2014-04-26 07:28:49
---
In logcat of Android Studio there is usually too much output, sometimes a developer would want to filter out these results so that he only gets logs from the application he is debugging. This can be achieved by the following method.
On the left side (right next to the tabs) is an icon with green arrows - it can be toggled on/off to display only logcat from the process selected in the list :)

<img class="aligncenter size-full wp-image-2635" src="http://dostmuhammad.com/wp-content/uploads/aJJJa.png" alt="aJJJa" width="458" height="302" />

<strong>UPDATE:</strong>
as of android studio ver 0.4.5 u will get messages from the app that is running only by default.  Log cat has a new option (ON by default) which creates an application filter automatically such that only the launched application's output is shown
&nbsp;