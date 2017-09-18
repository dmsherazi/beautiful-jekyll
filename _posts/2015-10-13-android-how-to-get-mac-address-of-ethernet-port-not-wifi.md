---
ID: 3399
post_title: 'Android: How to get MAC address of Ethernet port (not WiFi)'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/android-how-to-get-mac-address-of-ethernet-port-not-wifi/
published: true
post_date: 2015-10-13 05:46:52
---
There are some android devices that have an ethernet (LAN) port for example Android STB, Android powered door-phone monitors, etc. The regular way of getting MAC address is as follows
<pre>WifiManager manager = (WifiManager) getSystemService(Context.WIFI_SERVICE);
WifiInfo info = manager.getConnectionInfo();
String address = info.getMacAddress();
</pre>
Not to forget adding the following permission in the <code>AndroidManifest.xml </code>

<pre>&lt;uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/&gt;</pre>
The above method will give us the MAC address of WiFi. Assuming your Ethernet interface is eth0, to get the MAC address of Ethernet port we have to try opening and reading the file <code>/sys/class/net/eth0/address</code>. This can be Implemented as below.
<pre>public static String loadFileAsString(String filePath) throws java.io.IOException{
    StringBuffer data = new StringBuffer(1000);
    BufferedReader reader = new BufferedReader(new FileReader(filePath));
    char[] buf = new char[1024];
    int numRead=0;
    while((numRead=reader.read(buf)) != -1){
        String readData = String.valueOf(buf, 0, numRead);
        data.append(readData);
    }
    reader.close();
    return data.toString();
}

public String getMacAddress(){
    try {
        return loadFileAsString("/sys/class/net/eth0/address")
                .toUpperCase().substring(0, 17);
    } catch (IOException e) {
        e.printStackTrace();
        return null;
    }
}</pre>