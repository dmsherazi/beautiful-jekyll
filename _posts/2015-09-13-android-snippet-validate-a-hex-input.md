---
ID: 3358
post_title: 'Android snippet: validate a hex number input'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/android-snippet-validate-a-hex-input/
published: true
post_date: 2015-09-13 12:58:25
---
This is how you can validate a hex input in android code. The regex it makes use of can be used in other languages as well.

Validation steps are :
<ul>
	<li>check if the input is not null or zero length</li>
	<li>check if the input has even numbers as hex numbers are always even</li>
	<li>match the input with the validating regex.</li>
</ul>
<pre>public boolean validHexInput(String str) {

   if (str == null || str.length() == 0) {
      return false;
   }

   // length should be even number 
   // otherwise its not a valid hex 
   if (str.length() % 2 == 0) {
      String var1 = "(?i)[0-9a-f]+";
      return str.matches(var1);
 }

 return false;
}

</pre>