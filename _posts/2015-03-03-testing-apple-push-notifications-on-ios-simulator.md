---
ID: 3163
post_title: >
  Testing apple push notifications on iOS
  simulator
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/testing-apple-push-notifications-on-ios-simulator/
published: true
post_date: 2015-03-03 13:36:46
---
You can not send / receive apple push notifications on iOS simulator as Push notifications are not available in the simulator. They require a provisioning profile from iTunes Connect, and thus are required to be installed on a device.

In order to test your app's response to a push notification you either have to use a real device or you may use a library called <a href="https://github.com/acoomans/SimulatorRemoteNotifications">SimulatorRemoteNotifications</a>.

SimulatorRemoteNotifications is a library to send mock remote notifications to the iOS simulator.

It's pretty easy to send push via terminal:
<pre>echo -n '{"message":"message"}' | nc -4u -w1 localhost 9930
echo -n '{"aps":{"alert" : "message","badge" : 99,"sound" : "default"}, "myField" : 54758}'</pre>
The library extends UIApplication by embedding a mini server that listen for UDP packets containing JSON-formated payload, and a service to send notifications to the mini server. It also includes the iOS Simulator Notifications MacOSX app to help you send the mock notifications.

Note that SimulatorRemoteNotifications does not send notification through Apple's Push Service.

More details at <a href="https://github.com/acoomans/SimulatorRemoteNotifications">https://github.com/acoomans/SimulatorRemoteNotifications</a>

&nbsp;