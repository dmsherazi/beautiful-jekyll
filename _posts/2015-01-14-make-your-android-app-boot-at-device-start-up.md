---
ID: 2935
post_title: >
  make your android app boot at device
  start-up
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/make-your-android-app-boot-at-device-start-up/
published: true
post_date: 2015-01-14 14:40:21
---
If you want your app to start-up automatically when Android boots up you need to the following

#1: add the following to your android manifest file


https://gist.github.com/dmsherazi/aad7242969bd5e8f4d66

This will register for a boot complete receiver event and ask for its permission.

#2 Add a the following java class

https://gist.github.com/dmsherazi/053719ac51a831b8b404