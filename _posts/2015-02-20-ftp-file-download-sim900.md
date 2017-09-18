---
ID: 2982
post_title: 'upload/downlaod file from FTP using AT commands  (Sim900 + arduino)'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/ftp-file-download-sim900/
published: true
post_date: 2015-02-20 17:29:15
---
In the <a title="TCP connection over GPRS using SIM900 and similar modems using AT commands" href="http://dostmuhammad.com/blog/tcp-connection-over-gprs-using-sim900-and-similar-modems-using-at-commands/">previous post</a> I explained how to make a connection and send data via TCP connection on SIM900 and similar modems. This post is going to be about FTP connection. FTP stands for "file transfer protocol." FTP powers one of the fundamental Internet functions and is the prescribed method for the transfer of files between computers. It is also the easiest and most secure way to exchange files over the Internet.

Without going into much details I would show the related AT commands and brief description. Later I would include sample code for FTP upload/download using arduino and SIM900
<div class="postbody">
<div class="content">
<table class="stoker" cellspacing="0">
<tbody>
<tr>
<td><strong>AT command</strong></td>
<td><strong>Response</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td>AT+SAPBR</td>
<td>OK</td>
<td>Configures GPRS profile.</td>
</tr>
<tr>
<td>AT+FTPCID=1</td>
<td>OK</td>
<td>Selects profile 1 for FTP.</td>
</tr>
<tr>
<td>AT+FTPSERV=”****”</td>
<td>OK</td>
<td>Sets FTP server domain name or IP address. **** is the domain name or the IP.</td>
</tr>
<tr>
<td>AT+FTPPORT=***</td>
<td>OK</td>
<td>Sets FTP server port. *** is the port.</td>
</tr>
<tr>
<td>AT+FTPUN=”***”</td>
<td>OK</td>
<td>Sets user name for FTP server access. *** is the user name.</td>
</tr>
<tr>
<td>AT+FTPPW=”***”</td>
<td>OK</td>
<td>Sets password for FTP server access. *** is the password.</td>
</tr>
<tr>
<td>AT+FTPPUTNAME="****"</td>
<td>OK</td>
<td>Sets destiny name for the file.*** is the name of the file.</td>
</tr>
<tr>
<td>AT+FTPPUTPATH="****"</td>
<td>OK</td>
<td>Sets destiny file path. *** is the path of the file.</td>
</tr>
<tr>
<td>AT+FTPPUT</td>
<td>OK</td>
<td>Use to put a file into the FTP server.</td>
</tr>
<tr>
<td>AT+FTPGETNAME="****"</td>
<td>OK</td>
<td>Sets origin name for the file.*** is the name of the file.</td>
</tr>
<tr>
<td>AT+FTPGETPATH="****"</td>
<td>OK</td>
<td>Sets origin file path. *** is the path of the file.</td>
</tr>
<tr>
<td>AT+FTPGET</td>
<td></td>
<td>Use to get a file into the FTP server.</td>
</tr>
</tbody>
</table>
</div>
</div>
<dl class="postprofile"><dt></dt></dl>Make sure you have a server and note the ftp port, we would consider using the default port 21. Switch on your modem and make sure pin code is disabled or properly entered and that GPRS connection is available.
<ol>
	<li>Configure GPRS by sending <span style="color: #3366ff;">AT+SAPBR=3,1,"Contype","GPRS"r</span>  .</li>
	<li>Set APN by sending   <span style="color: #3366ff;">AT+SAPBR=3,1,"APN","your apn"r</span>  .replace your apn with APN for your network.</li>
	<li>Now set the username and password for the apn (replace username and password with correct values )
<span style="color: #3366ff;">AT+SAPBR=3,1,"USER","username"r  .</span>
<span style="color: #3366ff;"> AT+SAPBR=3,1,"PASS","password"r</span></li>
	<li>Connect to GPRS connection by sending <span style="color: #3366ff;">AT+SAPBR=1,1r</span>, when connected Modem will respond with <span style="color: #339966;">OK</span></li>
	<li>Now select profile 1 for FTP by sending <span style="color: #3366ff;">AT+FTPCID=1r</span></li>
	<li>Now set FTP server domain or ip using the command <span style="color: #3366ff;">AT+FTPSERV=ftp.yourserver.comr</span></li>
	<li>Set FTP port by <span style="color: #3366ff;">AT+FTPPORT=21r</span></li>
	<li>Now send FTP credentials using <span style="color: #3366ff;">AT+FTPUN=user_namer</span> and <span style="color: #3366ff;">AT+FTPPW="password"r</span></li>
	<li>To get a file from FTP send <span style="color: #3366ff;">AT+FTPGETNAME=file_namer</span></li>
	<li> Now set the path of the file <span style="color: #3366ff;">AT+FTPGETPATH=/path/r</span></li>
	<li>Now send <span style="color: #3366ff;">AT+FTPGET=1r</span> and wait for response from server, which starts with <span style="color: #339966;">+FTPGET:1,1</span></li>
	<li>To upload a file to FTP server send <span style="color: #3366ff;">AT+FTPPUTNAME=file_namer</span></li>
	<li>Now set path <span style="color: #3366ff;">AT+FTPPUTPATH=/pathr</span></li>
	<li>Now send <span style="color: #3366ff;">AT+FTPPUT=1</span> and wait for <span style="color: #339966;">+FTPPUT:1,1</span> after which you need to send the content of file to be uploaded.</li>
</ol>
<!--INFOLINKS_OFF-->
<pre class="minimize:true lang:c++ decode:true " title="Sample code for upload and download a file from FTP with arduino and SIM900">int8_t answer;
int onModulePin = 2;
char aux_str[30];

char incoming_data[120];

char test_str[ ]= "0000000011111111222222223333333344444444555555556666666677777777000000001111111122222222333333334444";

int data_size, aux;


void setup(){

    pinMode(onModulePin, OUTPUT);
    Serial.begin(115200);


    Serial.println("Starting...");
    power_on();

    delay(5000);

    Serial.println("Connecting to the network...");

    while( (sendATcommand("AT+CREG?", "+CREG: 0,1", 500)
            || sendATcommand("AT+CREG?", "+CREG: 0,5", 500)) == 0 );

    configure_FTP();

    uploadFTP();

    downloadFTP();

    Serial.print("Incoming data: ");
    Serial.println(incoming_data);
}


void loop(){

}


void configure_FTP(){

    sendATcommand("AT+SAPBR=3,1,"Contype","GPRS"", "OK", 2000);
    sendATcommand("AT+SAPBR=3,1,"APN","APN"", "OK", 2000);
    sendATcommand("AT+SAPBR=3,1,"USER","user_name"", "OK", 2000);
    sendATcommand("AT+SAPBR=3,1,"PWD","password"", "OK", 2000);

    while (sendATcommand("AT+SAPBR=1,1", "OK", 20000) != 1);
    sendATcommand("AT+FTPCID=1", "OK", 2000);
    sendATcommand("AT+FTPSERV="ftp.yourserver.com"", "OK", 2000);
    sendATcommand("AT+FTPPORT=21", "OK", 2000);
    sendATcommand("AT+FTPUN="user_name"", "OK", 2000);
    sendATcommand("AT+FTPPW="password"", "OK", 2000);

}


void uploadFTP(){

    sendATcommand("AT+FTPPUTNAME="file_name"", "OK", 2000);
    sendATcommand("AT+FTPPUTPATH="/path"", "OK", 2000);
    if (sendATcommand("AT+FTPPUT=1", "+FTPPUT:1,1,", 30000) == 1)
    {
        data_size = 0;
        while(Serial.available()==0);
        aux = Serial.read();
        do{
            data_size *= 10;
            data_size += (aux-0x30);
            while(Serial.available()==0);
            aux = Serial.read();
        }
        while(aux != 0x0D);

        if (data_size &gt;= 100)
        {
            if (sendATcommand("AT+FTPPUT=2,100", "+FTPPUT:2,100", 30000) == 1)
            {
                Serial.println(sendATcommand(test_str, "+FTPPUT:1,1", 30000), DEC);
                Serial.println(sendATcommand("AT+FTPPUT=2,0", "+FTPPUT:1,0", 30000), DEC);
                Serial.println("Upload done!!");
            }
            else
            {
                sendATcommand("AT+FTPPUT=2,0", "OK", 30000);
            }
        }
        else
        {
            sendATcommand("AT+FTPPUT=2,0", "OK", 30000);
        }
    }
    else
    {
        Serial.println("Error openning the FTP session");
    }
}

void downloadFTP(){

    int x = 0;

    sendATcommand("AT+FTPGETNAME="file_name"", "OK", 2000);
    sendATcommand("AT+FTPGETPATH="/path"", "OK", 2000);
    if (sendATcommand("AT+FTPGET=1 ", "+FTPGET:1,1", 30000) == 1)
    {
        do{
            if (sendATcommand2("AT+FTPGET=2,50", "+FTPGET:2,", "+FTPGET:1,", 30000) == 1)
            {
                data_size = 0;
                while(Serial.available()==0);
                aux = Serial.read();
                do{
                    data_size *= 10;
                    data_size += (aux-0x30);
                    while(Serial.available()==0);
                    aux = Serial.read();
                }while(aux != 0x0D);

                Serial.print("Data received: ");
                Serial.println(data_size);

                if (data_size &gt; 0)
                {
                    while(Serial.available() &lt; data_size);
                    Serial.read();

                    for (int y = 0; y &lt; data_size; y++)
                    {
                        incoming_data[x] = Serial.read();
                        x++;
                    }
                    incoming_data[x] = ' ';
                }
                else
                {
                    Serial.println("Download finished");
                }
            }
            else if (answer == 2)
            {
                Serial.println("Error from FTP");
            }
            else
            {
                Serial.println("Error getting the file");
                data_size = 0;
            }
        }while (data_size &gt; 0);
    }
    else
    {
        Serial.println("Error openning the FTP session");
    }
}




void power_on(){

    uint8_t answer=0;

    // checks if the module is started
    answer = sendATcommand("AT", "OK", 2000);
    if (answer == 0)
    {
        digitalWrite(onModulePin,HIGH);
        delay(3000);
        digitalWrite(onModulePin,LOW);

        while(answer == 0){     // Send AT every two seconds and wait for the answer
            answer = sendATcommand("AT", "OK", 2000);
        }
    }
}


int8_t sendATcommand(char* ATcommand, char* expected_answer, unsigned int timeout){

    uint8_t x=0,  answer=0;
    char response[100];
    unsigned long previous;

    memset(response, ' ', 100);    // Initialize the string

    delay(100);

    while( Serial.available() &gt; 0) Serial.read();    // Clean the input buffer

    Serial.println(ATcommand);    // Send the AT command


        x = 0;
    previous = millis();

    // this loop waits for the answer
    do{
        if(Serial.available() != 0){
            // if there are data in the UART input buffer, reads it and checks for the asnwer
            response[x] = Serial.read();
            //Serial.print(response[x]);
            x++;
            // check if the desired answer  is in the response of the module
            if (strstr(response, expected_answer) != NULL)
            {
                answer = 1;
            }
        }
    }
    // Waits for the asnwer with time out
    while((answer == 0) &amp;&amp; ((millis() - previous) &lt; timeout));

        return answer;
}

int8_t sendATcommand2(char* ATcommand, char* expected_answer1,
            char* expected_answer2, unsigned int timeout){

    uint8_t x=0,  answer=0;
    char response[100];
    unsigned long previous;

    memset(response, ' ', 100);    // Initialize the string

    delay(100);

    while( Serial.available() &gt; 0) Serial.read();    // Clean the input buffer

    Serial.println(ATcommand);    // Send the AT command


        x = 0;
    previous = millis();

    // this loop waits for the answer
    do{
        // if there are data in the UART input buffer, reads it and checks for the asnwer
        if(Serial.available() != 0){
            response[x] = Serial.read();
            x++;
            // check if the desired answer 1 is in the response of the module
            if (strstr(response, expected_answer1) != NULL)
            {
                answer = 1;
            }
            // check if the desired answer 2 is in the response of the module
            if (strstr(response, expected_answer2) != NULL)
            {
                answer = 2;
            }
        }
        // Waits for the asnwer with time out
    }while((answer == 0) &amp;&amp; ((millis() - previous) &lt; timeout));

        return answer;
}</pre>
<!--INFOLINKS_ON-->
&nbsp;