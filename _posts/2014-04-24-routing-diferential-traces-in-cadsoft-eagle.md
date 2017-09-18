---
ID: 2629
post_title: >
  Routing Diferential traces in Cadsoft
  Eagle
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/routing-diferential-traces-in-cadsoft-eagle/
published: true
post_date: 2014-04-24 19:38:47
---
Eagle supports basic differential routing. To make a pair of traces a differential  pair, both signals should have the same name with <strong>_N</strong> and <strong>_P</strong> at the end. For example <code>`MIC_N`</code> and <code>`MIC_P`</code>. When you try to route this signal it will be seen as a differential  pair and will be routed as one. This means that both the traces will be routed at the same time as shown in the image above. Wen one of the two traces is selected both will be routed at the same time. To route only one trace, click on the trace to route it and when both traces are selected press escape to only route the one you selected.