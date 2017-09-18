---
ID: 3546
post_title: validate ip address using regex
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/validate-ip-address-using-regex/
published: true
post_date: 2016-11-14 08:50:56
---
The code snippet below will check if the passed string is a valid IP address or not .
An Internet Protocol address (IP address) is a numerical label assigned to each device participating in a computer network that uses the Internet Protocol for communication. Read more about IP address <a href="https://en.wikipedia.org/wiki/IP_address">here</a>. This snippet will validate IP version 4 addresses.
<pre>/**
 * validate IP address
 * @param String IP address to verify
 * @return Boolean result
 */
public static Boolean isIP(String input) {
    if (input!= null && !input.isEmpty()) {
        //Regex
        String regex = "^((25[0-5])|(2[0-4]\\d)|(1\\d\\d)|([1-9]\\d)|\\d)(\\.((25[0-5])|(2[0-4]\\d)|(1\\d\\d)|([1-9]\\d)|\\d)){3}$";
        //check if input matches the regex
        if (text.matches(regex)) {
            // valid ip
            return true;
        } else {
            // invalid ip
            return false;
        }
    }
    // invalid input
    return false;
}  

</pre>