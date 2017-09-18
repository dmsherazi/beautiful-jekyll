---
ID: 3335
post_title: 'Android: Call to getLayoutInflater() outside activity'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/android-call-to-getlayoutinflater-outside-activity/
published: true
post_date: 2015-06-08 16:15:22
---
Some times we need the inflater outside activities in android . To get access to the inflator we may use the following code snippet. You can use this outside activities - all you need is to provide a <code>Context</code>:
<pre>LayoutInflater inflater = LayoutInflater.from(context);</pre>

the from function also checks with assert that you actually get an inflater back and throws an error otherwise - which will be much easier to deal with then a null pointer exception somewhere in the code.

An Alternate way is shown below but I recommend to use the above one:
<pre>LayoutInflater inflater = (LayoutInflater) context.getSystemService( Context.LAYOUT_INFLATER_SERVICE );</pre>
Then to retrieve your different widgets, you inflate a layout:
<pre>View view = inflater.inflate( R.layout.myNewInflatedLayout, null );
Button myButton = (Button) view.findViewById( R.id.myButton );
</pre>