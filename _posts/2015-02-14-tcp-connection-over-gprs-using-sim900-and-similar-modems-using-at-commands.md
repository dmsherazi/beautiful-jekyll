---
ID: 2980
post_title: >
  TCP connection over GPRS using SIM900
  and similar modems using AT commands
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/tcp-connection-over-gprs-using-sim900-and-similar-modems-using-at-commands/
published: true
post_date: 2015-02-14 11:05:56
---
GSM/GPRS modems are getting very common these days, as prices are getting cheaper and cheaper. Apart from providing SMS and call functions to my projects I also wanted to communicate via TCP.

Although there are many documents and blog posts to help but I have always found that they either are answers to specific problem faced by someone or not providing complete details.  In this post I would first explain the AT commands used in brief. You may connect your SIM900 to your computer via a serial/usb and test these commands. In the later part of this post I would include arduino example code.

AT commands for TCP/UDP Connection with example response and a brief description are given in the table below. Refer to the AT commands manual of your modem for details
<table class="stoker" cellspacing="0">
<tbody>
<tr>
<td><strong>AT command</strong></td>
<td><strong>Response</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr>
<td>AT</td>
<td> OK</td>
<td>test command. reply is OK</td>
</tr>
<tr>
<td>AT+CGATT?</td>
<td> +CGATT:n</td>
<td>checks if GPRS is attached? n=1 if attached</td>
</tr>
<tr>
<td>AT+CIPMUX=n</td>
<td> OK</td>
<td>use n as 0 for single connection
or use 1 for multiple connections</td>
</tr>
<tr>
<td>AT+CSTT="apn","username","pass"</td>
<td>OK</td>
<td>Sets APN, user name and password</td>
</tr>
<tr>
<td>AT+CIICR</td>
<td> OK</td>
<td>Brings up wireless connection</td>
</tr>
<tr>
<td>AT+CIFSR</td>
<td> ip address</td>
<td>Get local IP address if connected</td>
</tr>
<tr>
<td>AT+CIPSTART=“TYPE” , “domain”, “port”</td>
<td> Connected</td>
<td>Establishes a connection with a server. Type can be UDP or TCP</td>
</tr>
<tr>
<td>AT+CIPSEND</td>
<td> &gt;</td>
<td>Sends data when the a connection is established.</td>
</tr>
<tr>
<td>AT+CIPCLOSE</td>
<td> OK</td>
<td>Closes the connection</td>
</tr>
<tr>
<td>AT+CIPSHUT</td>
<td> SHUT OK</td>
<td>resets IP session if any</td>
</tr>
</tbody>
</table>
how to make a connection:
<!--INFOLINKS_OFF-->
<ol>
	<li>Send <span style="color: #339966;"><em>ATr</em></span> and wait for a response from the modem. You should recieve <em><span style="color: #3366ff;">OK</span></em>
if everything is set.</li>
	<li>Make sure that the Modem has registered to network and that PIN code is disabled on the SIM. Send <em><span style="color: #339966;">AT+CGATT?r</span></em> to check if GPRS is attached or not.  <em><span style="color: #3366ff;">+CGATT: 1</span></em> indicates that GPRS is attached.</li>
	<li>Send <em><span style="color: #339966;">AT+CIPSHUTr</span></em> . Although its optional this will be helpful as it resets IP session if any. you will get a response <em><span style="color: #3366ff;">SHUT OK</span> </em>.</li>
	<li>Send <span style="color: #339966;"><em>AT+CIPMUX=0</em></span> to set a single connection mode, response would be <em><span style="color: #3366ff;">OK</span></em></li>
	<li>Now set APN settings by <span style="color: #339966;"><em>AT+CSTT= “apn ”, “username”, “password”r</em></span> . replace apn, username and password to match APN (Access Point Name) ,username and password for your service provider.</li>
	<li>Now send <em><span style="color: #339966;">AT+CIICRr</span></em> , this will bring up the wireless connection. <em><span style="color: #3366ff;">OK</span></em> is received on successful connection</li>
	<li>Send <em><span style="color: #339966;">AT+CIFSRr</span></em> , this will reply with the IP address the modem has been assigned.</li>
	<li>Send <em><span style="color: #339966;">AT+CIPSTART="TCP","server domain name or ip","port"r</span></em>, replace the domain name/ip and port with appropriate values, on connection modem will reply with <em><span style="color: #3366ff;">CONNECT OK</span></em></li>
	<li>Now you can send your data using <em><span style="color: #339966;">AT+CIPSENDr</span> </em> AT command. modem will respond with <em><span style="color: #3366ff;">&gt;</span></em> indicating it is ready to receive data to be sent. Type in your data.</li>
	<li>Now the modem is waiting for the <em><span style="color: #339966;">ASCII 26</span> </em> that is <span style="color: #339966;">control+z</span> on keyboard. Depending on the terminal software used you can either press control and Z together on keyboard or send hex value <span style="color: #339966;">0x1A</span>. The modem will then send the response from server.</li>
	<li>Now send <em><span style="color: #339966;">AT+CIPSHUT</span></em> to shut down the connection. Modem will reply with <span style="color: #3366ff;">SHUT OK </span></li>
	<li>cheers :)</li>
</ol>
ARDUINO CODE :

Below is example code for single and multiple connection using arduino and sim900
<pre class="font-size-enable:false toolbar-delay:false minimize:true lang:c++ decode:true " title="example code for single connection using arduino and sim900 CLICK TO EXPAND">int8_t answer;
int onModulePin= 2;
char aux_str[50];
char ip_data[40]="Test string from GPRS shieldrn";
void setup(){
    pinMode(onModulePin, OUTPUT);
    Serial.begin(115200);
    Serial.println("Starting...");
    power_on();
    delay(3000);
    // sets the PIN code
    sendATcommand2("AT+CPIN=****", "OK", "ERROR", 2000);
    delay(3000);
    Serial.println("Connecting to the network...");
    while( sendATcommand2("AT+CREG?", "+CREG: 0,1", "+CREG: 0,5", 1000)== 0 );
}
void loop(){
    // Selects Single-connection mode
    if (sendATcommand2("AT+CIPMUX=0", "OK", "ERROR", 1000) == 1)
    {
        // Waits for status IP INITIAL
        while(sendATcommand2("AT+CIPSTATUS", "INITIAL", "", 500)  == 0 );
        delay(5000);

        // Sets the APN, user name and password
        if (sendATcommand2("AT+CSTT="APN","user_name","password"", "OK",  "ERROR", 30000) == 1)
        {
            // Waits for status IP START
            while(sendATcommand2("AT+CIPSTATUS", "START", "", 500)  == 0 );
            delay(5000);

            // Brings Up Wireless Connection
            if (sendATcommand2("AT+CIICR", "OK", "ERROR", 30000) == 1)
            {
                // Waits for status IP GPRSACT
                while(sendATcommand2("AT+CIPSTATUS", "GPRSACT", "", 500)  == 0 );
                delay(5000);

                // Gets Local IP Address
                if (sendATcommand2("AT+CIFSR", ".", "ERROR", 10000) == 1)
                {
                    // Waits for status IP STATUS
                    while(sendATcommand2("AT+CIPSTATUS", "IP STATUS", "", 500)  == 0 );
                    delay(5000);
                    Serial.println("Openning TCP");

                    // Opens a TCP socket
                    if (sendATcommand2("AT+CIPSTART="TCP","IP_address","port"",
                            "CONNECT OK", "CONNECT FAIL", 30000) == 1)
                    {
                        Serial.println("Connected");

                        // Sends some data to the TCP socket
                        sprintf(aux_str,"AT+CIPSEND=%d", strlen(ip_data));
                        if (sendATcommand2(aux_str, "&gt;", "ERROR", 10000) == 1)
                        {
                            sendATcommand2(ip_data, "SEND OK", "ERROR", 10000);
                        }

                        // Closes the socket
                        sendATcommand2("AT+CIPCLOSE", "CLOSE OK", "ERROR", 10000);
                    }
                    else
                    {
                        Serial.println("Error openning the connection");
                    }
                }
                else
                {
                    Serial.println("Error getting the IP address");
                }
            }
            else
            {
                Serial.println("Error bring up wireless connection");
            }
        }
        else
        {
            Serial.println("Error setting the APN");
        }
    }
    else
    {
        Serial.println("Error setting the single connection");
    }

    sendATcommand2("AT+CIPSHUT", "OK", "ERROR", 10000);
    delay(10000);
}

void power_on(){

    uint8_t answer=0;

    // checks if the module is started
    answer = sendATcommand2("AT", "OK", "OK", 2000);
    if (answer == 0)
    {
        // power on pulse
        digitalWrite(onModulePin,HIGH);
        delay(3000);
        digitalWrite(onModulePin,LOW);

        // waits for an answer from the module
        while(answer == 0){     // Send AT every two seconds and wait for the answer
            answer = sendATcommand2("AT", "OK", "OK", 2000);
        }
    }

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
            // check if the desired answer 1  is in the response of the module
            if (strstr(response, expected_answer1) != NULL)
            {
                answer = 1;
            }
            // check if the desired answer 2 is in the response of the module
            else if (strstr(response, expected_answer2) != NULL)
            {
                answer = 2;
            }
        }
    }
    // Waits for the asnwer with time out
    while((answer == 0) &amp;&amp; ((millis() - previous) &lt; timeout));

    return answer;
}</pre>
<pre class="font-size-enable:false minimize:true lang:c++ decode:true " title="example code for multople connection using arduino and sim900  CLICK TO EXPAND">int8_t answer;
int onModulePin= 2;
char aux_str[50];

char ip_data[40]="Test string from GPRS shieldrn";

void setup(){

    pinMode(onModulePin, OUTPUT);
    Serial.begin(115200);

    Serial.println("Starting...");
    power_on();

    delay(3000);

    // sets the PIN code
    sendATcommand2("AT+CPIN=****", "OK", "ERROR", 2000);

    delay(3000);

    Serial.println("Connecting to the network...");

    while( sendATcommand2("AT+CREG?", "+CREG: 0,1", "+CREG: 0,5", 1000) == 0 );

}


void loop(){


    // Selects Multi-connection mode
    if (sendATcommand2("AT+CIPMUX=1", "OK", "ERROR", 1000) == 1)
    {
        // Waits for status IP INITIAL
        while(sendATcommand2("AT+CIPSTATUS", "INITIAL", "", 500)  == 0 );
        delay(5000);

        // Sets the APN, user name and password
        if (sendATcommand2("AT+CSTT="APN","user_name","password"", "OK",  "ERROR", 30000) == 1)
        {
            // Waits for status IP START
            while(sendATcommand2("AT+CIPSTATUS", "START", "", 500)  == 0 );
            delay(5000);

            // Brings Up Wireless Connection
            if (sendATcommand2("AT+CIICR", "OK", "ERROR", 30000) == 1)
            {
                // Waits for status IP GPRSACT
                while(sendATcommand2("AT+CIPSTATUS", "GPRSACT", "", 500)  == 0 );
                delay(5000);

                // Gets Local IP Address
                if (sendATcommand2("AT+CIFSR", ".", "ERROR", 10000) == 1)
                {
                    // Waits for status IP STATUS
                    while(sendATcommand2("AT+CIPSTATUS", "IP STATUS", "", 500)  == 0 );
                    delay(5000);
                    Serial.println("Openning TCP");

                    // Opens a TCP socket with connection 1
                    if (sendATcommand2("AT+CIPSTART=1,"TCP","IP_address","port"",
                                    "CONNECT OK", "CONNECT FAIL", 30000) == 1)
                    {
                        Serial.println("Connected");

                        // Sends some data to the TCP socket
                        sprintf(aux_str,"AT+CIPSEND=1,%d", strlen(ip_data));
                        if (sendATcommand2(aux_str, "&gt;", "ERROR", 10000) == 1)
                        {
                            delay(500);
                            sendATcommand2(ip_data, "SEND OK", "ERROR", 10000);
                        }

                        // Closes the socket
                        sendATcommand2("AT+CIPCLOSE=1", "CLOSE OK", "ERROR", 10000);
                    }
                    else
                    {
                        Serial.println("Error openning the connection 1");
                    }

                }
                else
                {
                    Serial.println("Error getting the IP address");
                }
            }
            else
            {
                Serial.println("Error bring up wireless connection");
            }
        }
        else
        {
            Serial.println("Error setting the APN");
        }
    }
    else
    {
        Serial.println("Error setting the multi-connection");
    }

    sendATcommand2("AT+CIPSHUT", "OK", "ERROR", 10000);
    delay(10000);
}

void power_on(){

    uint8_t answer=0;

    // checks if the module is started
    answer = sendATcommand2("AT", "OK", "OK", 2000);
    if (answer == 0)
    {
        // power on pulse
        digitalWrite(onModulePin,HIGH);
        delay(3000);
        digitalWrite(onModulePin,LOW);

        // waits for an answer from the module
        while(answer == 0){     // Send AT every two seconds and wait for the answer
            answer = sendATcommand2("AT", "OK", "OK", 2000);
        }
    }

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
            // check if the desired answer 1  is in the response of the module
            if (strstr(response, expected_answer1) != NULL)
            {
                answer = 1;
            }
            // check if the desired answer 2 is in the response of the module
            else if (strstr(response, expected_answer2) != NULL)
            {
                answer = 2;
            }
        }
    }
    // Waits for the asnwer with time out
    while((answer == 0) &amp;&amp; ((millis() - previous) &lt; timeout));

    return answer;
}</pre>
<!--INFOLINKS_ON-->