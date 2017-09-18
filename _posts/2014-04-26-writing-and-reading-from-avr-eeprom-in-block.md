---
ID: 2639
post_title: >
  writing and reading from AVR EEPROM in
  Block.
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/writing-and-reading-from-avr-eeprom-in-block/
published: true
post_date: 2014-04-26 08:29:29
---
EEPROM can be used to store non volatile data of the program , sometimes you need to write arrays even multidimensional. The way I do it is by using EEMEM attribute. EMMEM is used to allocate space in EEPROM.

I use the Macros given below to write or read to EEPROM.  you have to use #include <avr /eeprom.h> I would be precise . below is the Code.

<pre>
#include

//////////////////////////////////////////////////////////////////////////
//        Macros and # Defines
//write block to EEPROM
#define eepw(message,EEADDR,BLKSIZE) eeprom_write_block((const void*)message,(void*)EEADDR,BLKSIZE);
//read block from EEPROM
#define eepr(readblck,EEADDR,BLKSIZE) eeprom_read_block((void*)readblck,(const void*)EEADDR,BLKSIZE);

uint8_t EEMEM eepstring[15];
</pre>
Example use
<pre>eepw("sample test 1",eestring, 15);  // "writes sample test1" to eestring in EEprom ,
char d[15];   //array in ram
eeprom_read(d, eestring[0],15); // reads the data and puts it in d[]</pre></avr>