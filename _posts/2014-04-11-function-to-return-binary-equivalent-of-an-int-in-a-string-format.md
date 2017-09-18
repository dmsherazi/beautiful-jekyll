---
ID: 2513
post_title: >
  function to return binary equivalent of
  an int in a string format
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/function-to-return-binary-equivalent-of-an-int-in-a-string-format/
published: true
post_date: 2014-04-11 18:17:16
---
On request of Shamas Akhtar Awan :
This is the function to return a string of binary equivalent of an int. The function takes in an integer value and returns a string of 0′s and 1′s of binary equavalet of that integer.
<pre class="brush:cpp ">char * int2binarystr(int value) {
    char binstr[23];// adjust the size of the string to your needs
    int i,b;
    b=value;
    i=0;
    while(b&gt;0)
    {
        binstr[i]=b%2;
        b=b/2; i++;
    }
    binstr[i]=00;
    return binstr; // returns the string
}</pre>
You can use this in your code as needed. One example is to write to uart the string
<pre class="brush:cpp">Uart0_write_text(int2binarystr(20)); // writes the string conataing the binary equavalent of 20 to uart</pre>