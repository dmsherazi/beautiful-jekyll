---
ID: 2791
post_title: How to change ip address in linux
author: Shoaib Ahmed
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/how-to-change-ip-address-in-linux/
published: true
post_date: 2015-05-21 13:23:46
---
I wrote this draft quite ago . Just stumbled upon on it in the drafts section, may this would help someone
<h3>Change IP address</h3>
You can change ip address using ifconfig command itself. To set IP address 192.168.1.5, enter command:

<code># ifconfig eth0 192.168.1.5 netmask 255.255.255.0 up
# ifconfig eth0
</code>

To make permanent changes to IP address you need to edit configuration file according to your Linux distribution.

Here are some detailed posts:
<ul>
	<li><a href="http://www.cyberciti.biz/faq/linux-change-ip-address/">http://www.cyberciti.biz/faq/linux-change-ip-address/</a></li>
	<li><a href="https://www.linode.com/docs/networking/linux-static-ip-configuration">https://www.linode.com/docs/networking/linux-static-ip-configuration</a></li>
	<li><a href="http://www.wikihow.com/Assign-an-IP-Address-on-a-Linux-Computer">http://www.wikihow.com/Assign-an-IP-Address-on-a-Linux-Computer</a></li>
</ul>