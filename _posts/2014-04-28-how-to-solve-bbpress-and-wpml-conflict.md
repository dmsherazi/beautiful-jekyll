---
ID: 2647
post_title: How to solve bbPress and WPML conflict!
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/how-to-solve-bbpress-and-wpml-conflict/
published: true
post_date: 2014-04-28 06:55:45
---
I use <a href="https://wpml.org/">WPML </a>on one of WordPress site I developed for my company. recently I installed <a href="http://bbpress.org/">bbpress </a>plugin to incorporate a forum on the same website. When I used both plugin together I found that I couldn't reply or create a new topic. It was strange that suddenly the Forum, topics and reply (All the elements added by bbpress to wp-admin menu bar ) were hidden.<!--more-->

I started by googling about it and the first thing I learnt was that there were a number of plugins that are not compatible with bbpress (or bbpress isn't compatible with). So I deactivated all plugins and then activated them one by one. I found that WPML Multilingual CMS plugin was incompatible.

There are a number of people complaining the same issue both at <a href="http://bbpress.org/forums">bbpress support forums</a> as well as <a href="http://wpml.org/forums/">WPML support forums</a>. There are a number of threads but mostly wont have any working solution.

Here is the solution. In order to use WPML and bbpress together you need to have bbpress Multilingual Plugin which still isn't provided by WPML with its package. You can get a fork of it on one of the Git-hub repositories <strong><a class="js-current-repository js-repo-home-link" style="color: #4183c4;" href="https://github.com/dmsherazi/bbPress-Multilingual">bbPress-Multilingual</a></strong>
.

Installed this plugin and Hurray... !