---
ID: 2696
post_title: 'STM32 Microcontrollers &#8211; Prior to Start'
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/stm32-microcontrollers-prior-to-start/
published: true
post_date: 2014-06-14 05:35:46
---
<p style="text-align: left;">STM32 <a class="zem_slink" title="ARM architecture" href="http://www.arm.com" target="_blank" rel="homepage">ARM-based</a> micros from <a class="zem_slink" title="STMicroelectronics" href="http://www.st.com/" target="_blank" rel="homepage">STMicroelectronics</a> pack high density resources than any other conventional microcontroller. They are also high speed devices, operating typically at 72MHz and beyond. Despite several advanced features and heavy resources, they turn out to be misfortunes for beginners who wish to play with them. Available in market are several cool STM32 boards but most of them are not well documented. The aim of this document is to address some common <a class="zem_slink" title="FAQ" href="http://en.wikipedia.org/wiki/FAQ" target="_blank" rel="wikipedia">FAQs</a>.</p>
Typically most people ask the following question:
<ul>
	<li>How to program the STM32 micro embedded in my development board?</li>
	<li>What tools do I need to get started?</li>
	<li>What compiler support do I have for STM32?</li>
	<li>What resources are available for STM32 on the internet?</li>
</ul>
<!--more-->

In this doc, I’ll be addressing these FAQs along with some basics as I had similar questions in my early expeditions with STM32 micros. When I started with STM32 these questions were there as they are now. Literally there was nothing to address them till now. Most experts take it for granted that those who are beginning with ARMs must have heavy knowledge on the topic and thus skip answering these simple or silly questions.

Well I decided to break this stalemate for any starter no matter what’s his/her experience. Firstly most people nowadays believe ARM is only for mobile phones, <a class="zem_slink" title="Personal digital assistant" href="http://en.wikipedia.org/wiki/Personal_digital_assistant" target="_blank" rel="wikipedia">PDAs</a>, tablets, etc. and can’t be used like other micros like <a class="zem_slink" title="Atmel AVR" href="http://en.wikipedia.org/wiki/Atmel_AVR" target="_blank" rel="wikipedia">AVRs</a> and PICs. This is completely wrong. Firstly because no one has set such a rule and secondly because there’s no limit to requirements in an embedded design. However it would be wasteful to make simple LED blinking stuffs with such chips. When it comes to size and resources ARM varies in all aspects. You can have an ARM chip with similar resources available in a typical 8 bit or 16 bit micro and yet you can also have an ARM chip with high resources. For instance if you think of flash memory, an ARM chip can have a few kilobytes to several megabytes of flash memory. Thus not just for real-time operating systems, phones, DSP, graphical processing and so on but also for other kinds of embedded systems the door for ARM is always open. It’ll completely depend on its user. STM32 portfolio has wide ranges of 32 bit ARM micros just as I described. A quick look on ST’s page will give you a brief idea: <a href="http://www.st.com/web/en/catalog/mmc/FM141/SC1169">http://www.st.com/web/en/catalog/mmc/FM141/SC1169</a> .

&nbsp;

Answering from the last, let’s see what resources are available for STM32s on the internet. Going back to ST’s site one can clearly see that there are several app notes for STM32s. At the time of writing this doc there 83 app notes on ST’s page. Obviously then there are reference manuals, datasheet and other docs too. Of these the important ones are the datasheet of a particular micro and its family reference manual. The rest of the stuffs are various software and tools but here confusion arises. We’ll see what other things are needed later but for now let’s see the purpose of reference manuals and datasheet. The reference manual is needed for understanding the internal hardware of a particular STM32 family, the registers associated with these hardware, programming techniques and what “not”s and what “are”s. These make it the core document of all. Datasheet basically give overviews of the devices. Books available for STM32-based ARMs are hard to find but still found a book called Discovering STM32 on Google search’s first page.

Regarding compiler selection, there are several available for STM32 micros. The most common ones are Keil, CooCox and MikroC PRO for ARM. My personal favourite is MikroC (<a href="http://www.mikroe.com/mikroc/arm/">http://www.mikroe.com/mikroc/arm/</a>) as I’m already familiar with MikroC for AVR and 8051. MikroC comes with lot of easy-to-use built-in and examples and so it’s a good compiler to work with. Anyone familiar with MikroC will not have any trouble using it for ARM. With MikroC one can go to raw levels and he/she can also go for easy library-based coding.

Now let’s see what tools we’ll need for STM32 micros. The first tool we’ll need is called Flash Loader Demonstrator (<a href="http://www.st.com/web/en/catalog/tools/PF257525">http://www.st.com/web/en/catalog/tools/PF257525</a>).  Basically it’s a programmer <a class="zem_slink" title="Graphical user interface" href="http://en.wikipedia.org/wiki/Graphical_user_interface" target="_blank" rel="wikipedia">GUI</a> based on factory loaded bootloader that allows a user to load, erase, verify, read or set configuration bits for his/her STM32 micro. The second tool is called Microxplorer (<a href="http://www.st.com/web/en/catalog/tools/PF251717">http://www.st.com/web/en/catalog/tools/PF251717</a>). This tool allows a user to graphically set configurations for IO ports, internal hardware and many more. Basically it’ll help you reduce your time debugging registers. Both of these software are free and easy to use.  The last but not the least tool is called Timer Calculator (<a href="http://www.libstock.com/projects/view/398/timer-calculator">http://www.libstock.com/projects/view/398/timer-calculator</a>). It’s a handy tool for those who’ll use MikroC for ARM. It can be used to generate codes for timer interrupts and timer-based stuffs. There are other tools too.

The final topic is about loading code to a STM32 micro. There are two ways either by a <a class="zem_slink" title="Joint Test Action Group" href="http://en.wikipedia.org/wiki/Joint_Test_Action_Group" target="_blank" rel="wikipedia">JTAG</a> programmer like ST-Link or by bootloader and <a class="zem_slink" title="Universal asynchronous receiver/transmitter" href="http://en.wikipedia.org/wiki/Universal_asynchronous_receiver/transmitter" target="_blank" rel="wikipedia">UART</a>. The former is the best choice as it is a programmer and a debugger but in terms of expense this is unnecessary as the chips come with preprogramed bootloader. Thus the latter method of using bootloader and UART is simplest and also the most popular solution. This is also my personal preference as I didn’t want to spend for another programmer just for the purpose studying. This is the method I’ll describe here. Let’s see the board:
<p align="center"><a href="http://dostmuhammad.com/wp-content/uploads/KGrHqNHJBsFHeN22JdBR36hs-g60_12.jpg"><img class="aligncenter wp-image-2698 size-full" src="http://dostmuhammad.com/wp-content/uploads/KGrHqNHJBsFHeN22JdBR36hs-g60_12-e1402724499698.jpg" alt="$(KGrHqNHJBsFHeN22Jd)BR36)hs)-g~~60_12" width="500" height="363" /></a></p>
&nbsp;

This baby is about the size of a standard match box and contains the basic components needed for its STM32F108C8 micro. This one comes from LC-Technology <a class="zem_slink" title="China" href="http://maps.google.com/maps?ll=39.9166666667,116.383333333&amp;spn=10.0,10.0&amp;q=39.9166666667,116.383333333 (China)&amp;t=h" target="_blank" rel="geolocation">China</a> (<a href="http://www.lctech-inc.com/Hardware/Detail.aspx?id=0172e854-77b0-43d5-b300-68e570c914fd">http://www.lctech-inc.com/Hardware/Detail.aspx?id=0172e854-77b0-43d5-b300-68e570c914fd</a>) and is reasonably cheap. I have also other ARM boards but this one is my favourite because of its compact size and portability. Most STM32F10x board have similar features and no matter what board is chosen there’ll literally no difference at all.

Now let’s see the important parts of the board:

&nbsp;

<a href="http://dostmuhammad.com/wp-content/uploads/hz-fileserver-upload1_hj0zu1t8.jpg"><img class="aligncenter size-full wp-image-2699" src="http://dostmuhammad.com/wp-content/uploads/hz-fileserver-upload1_hj0zu1t8.jpg" alt="hz-fileserver-upload1_hj0zu1t8" width="700" height="700" /></a>

&nbsp;

These are the least common features of any STM32 development board must have.

&nbsp;

<a href="http://dostmuhammad.com/wp-content/uploads/hz-fileserver-upload1_hj0zu1tb.jpg"><img class="aligncenter size-full wp-image-2700" src="http://dostmuhammad.com/wp-content/uploads/hz-fileserver-upload1_hj0zu1tb.jpg" alt="hz-fileserver-upload1_hj0zu1tb" width="700" height="700" /></a>

&nbsp;

Here’s the schematic of the board:

&nbsp;

<img class="aligncenter" src="http://www.olliw.eu/uploads/lctech-stm32-devboard-scheme-01-wp01.png" alt="lctech-stm32-devboard-sch" width="6481" height="4252" />

&nbsp;

To demonstrate Flash Loader Demonstrator I made a setup for a wasteful LED blinking project with STM32 just for the sake of giving a demo. Here’s the setup:

<a href="http://embedded-lab.com/blog/?attachment_id=8768" rel="attachment wp-att-8768"><img class="aligncenter size-full wp-image-8768" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/setup.png" alt="setup" width="601" height="358" /></a>

The needed tools here are a PC, a FT232 USB-UART converter, a LED breakout board and of course a STM32 board. Since the micro is empty the LEDs are all off. Now let’s upload a code in it. Before we do that please have a look in “Boot Configuration” section of STM32F103’s reference manual and also locate the boot jumpers of your board. Usually <i>Boot 0</i> is kept low and <i>Boot 1</i> high to enter bootloader mode after reset.

&nbsp;

<a href="http://dostmuhammad.com/wp-content/uploads/Capture6.png"><img class="aligncenter size-full wp-image-2717" src="http://dostmuhammad.com/wp-content/uploads/Capture6.png" alt="Capture" width="586" height="270" /></a>

The first photo below shows the jumper settings during normal running and the second shows the settings needed during uploading code. Every time the jumpers are altered a reset is a must. To do so just hit the reset switch briefly.

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8770" rel="attachment wp-att-8770"><img class="aligncenter size-full wp-image-8770" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/setup2.png" alt="setup2" width="716" height="464" /></a>

&nbsp;

Be sure to change jumpers when changing modes. Shown below are step-step ways of loading a code using boot loader and UART. Prior to entering boot loader mode change the jumper and hold reset before clicking “Next” in the Flash Loader Demonstrator GUI. This is similar to entering the boot loader mode of an Arduino but manually.

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8772" rel="attachment wp-att-8772"><img class="aligncenter size-full wp-image-8772" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/setup22.png" alt="setup2" width="862" height="324" /></a>

&nbsp;

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8773" rel="attachment wp-att-8773"><img class="aligncenter size-full wp-image-8773" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/screen2.png" alt="screen2" width="849" height="451" /></a>

&nbsp;

&nbsp;

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8774" rel="attachment wp-att-8774"><img class="aligncenter size-full wp-image-8774" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/screen3.png" alt="screen3" width="874" height="334" /></a>

&nbsp;

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8775" rel="attachment wp-att-8775"><img class="aligncenter size-full wp-image-8775" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/screen4.png" alt="screen4" width="851" height="673" /></a>

&nbsp;

&nbsp;

&nbsp;

After flashing the STM32, the code runs as shown below:

&nbsp;

<a href="http://embedded-lab.com/blog/?attachment_id=8776" rel="attachment wp-att-8776"><img class="aligncenter size-full wp-image-8776" src="http://embedded-lab.com/blog/wp-content/uploads/2014/06/out.png" alt="out" width="328" height="193" /></a>

&nbsp;

I hope it was helpful. Happy coding.

<i>Contributed by: Shawon M. Shahryiar</i>

<a href="https://www.facebook.com/MicroArena?ref=hl"><i>https://www.facebook.com/MicroArena</i></a>

https://www.facebook.com/sshahryiar

<i><a href="mailto:sshahryiar@gmail.com">sshahryiar@gmail.com</a></i>

<i>+8801970046495   </i>

&nbsp;