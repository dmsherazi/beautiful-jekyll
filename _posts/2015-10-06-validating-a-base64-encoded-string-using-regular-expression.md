---
ID: 3390
post_title: >
  validating a base64 encoded string using
  regular expression
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/validating-a-base64-encoded-string-using-regular-expression/
published: true
post_date: 2015-10-06 17:00:32
---
We can validate a base64 encoded string using a nice regex (regular expression). The following regex can be used with any programming language. I would use php for the example. The regex is as follows.
<pre>^[a-zA-Z0-9/+]*={0,2}$</pre>
Which will also detect the usage of = or == at the end of the string (and only end).

A function geared specifically toward this:
<pre><span class="default">&lt;?php</span><span class="keyword">function </span><span class="default">is_base64_encoded</span><span class="keyword">()
 {
     if (</span><span class="default">preg_match</span><span class="keyword">(</span><span class="string">'%^[a-zA-Z0-9/+]*={0,2}$%'</span><span class="keyword">, </span><span class="default">$data</span><span class="keyword">)) {
           return </span><span class="default">TRUE</span><span class="keyword">;
      } 
     else {
             return </span><span class="default">FALSE</span><span class="keyword">;
       }
 };
</span><span class="default"> is_base64_encoded</span><span class="keyword">(</span><span class="string">"iash21iawhdj98UH3"</span><span class="keyword">); </span><span class="comment">// true
 </span><span class="default">is_base64_encoded</span><span class="keyword">(</span><span class="string">"#iu3498r"</span><span class="keyword">); </span><span class="comment">// false
 </span><span class="default">is_base64_encoded</span><span class="keyword">(</span><span class="string">"asiudfh9w=8uihf"</span><span class="keyword">); </span><span class="comment">// false
 </span><span class="default">is_base64_encoded</span><span class="keyword">(</span><span class="string">"a398UIhnj43f/1!+sadfh3w84hduihhjw=="</span><span class="keyword">); </span><span class="comment">// false
</span><span class="default">?&gt;</span></pre>