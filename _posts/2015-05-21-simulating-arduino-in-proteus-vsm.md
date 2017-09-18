---
ID: 3068
post_title: Simulating Arduino in Proteus VSM
author: Dost Muhammad Shah
post_excerpt: ""
layout: post
permalink: >
  http://dostmuhammad.com/blog/simulating-arduino-in-proteus-vsm/
published: true
post_date: 2015-05-21 13:45:21
---
<header> This is an old post which I am reposting... also <a href="http://dostmuhammad.com/simulating-arduino-mega2560-in-proteus/">check Simulating Arduino Mega2560 in Proteus.</a>

Arduino platform is a great tool for everyone who wants to play with microcontrollers in a simple and inexpensive way. It offers perhaps the quickest and easiest ways to do cool stuffs with its rich built-in library and easy to grasp interface. It’s also open-source and for this reason there are many open-source projects with it in the Internet. I have personally enjoyed it a lot. Although Arduino is pretty popular amongst many users, there is no good simulator software for it. Proteus VSM, on the other hand, is a very good circuit simulator software. However it lacks a model or simulator primitive for Arduino. Thus simulating Arduino in Proteus is in a way impossible. If these powerful tools can be synced together then a lot of new possibilities will arise. This is what I wondered from day one of Arduinoing. In this doc we will discuss how to integrate these software and simulate Arduino in Proteus.In Proteus we need to add a .hex or .coff file in a micro in order to simulate its behaviour. However Arduino works with .ino or .pde files and the folders that hold Arduino sketches don’t contain .hex or .coff files. Thus there’s no straight way. Now if there’s no straight path then we have to go around.Firstly we have to make a suitable Proteus schematic like the one shown. You can also download a template provided at the end of post.

</header><section class="entry"><img class=" size-medium wp-image-3297 alignnone" src="http://dostmuhammad.com/wp-content/uploads/2015/05/405495_1826120830872_733664937_n-300x109.jpg" alt="405495_1826120830872_733664937_n" />Once the schematic is completed, we have to set the fuses and clock frequency as shown

<img class="alignnone size-medium wp-image-3298" src="http://dostmuhammad.com/wp-content/uploads/2015/05/429053_1826118790821_849601661_n-300x156.jpg" alt="429053_1826118790821_849601661_n" />

<!--more-->

Our schematic is ready for Arduinoing. Now we need to upload code for the Arduino in Proteus. To do that we will firstly need to change our folder options in a way that hidden files are no longer hidden. In Windows OS, we have to go to Control Panel and then click Folder Options icon. When the Folder Options window opens, we need to click the View tab and select “Show hidden files, folder and drives”. We must now apply the changes and exit the Folder Options window. We are now just one step behind completing our goal. At this point, we have to open the Arduino IDE and save our sketch at our desired location with our desired name. This is however not mandatory. In our example, we have used the ready-made Blink example provided with the Arduino IDE.

<a href="http://dostmuhammad.com/wp-content/uploads/2015/05/401401_1826119030827_1361340838_n.jpg"><img class="alignnone size-medium wp-image-3299" src="http://dostmuhammad.com/wp-content/uploads/2015/05/401401_1826119030827_1361340838_n-300x160.jpg" alt="401401_1826119030827_1361340838_n" /></a>

It’s necessary that no Arduino board is connected to the PC where we will do the simulation or if it is connected we have change port settings in the IDE so that the code is not uploaded to the board. Next we hit the verify and upload buttons of the IDE. At this point we will be getting an error. This is okay and we are looking for this error. When this error happens, we will get the folder location of the hex file that was about to be uploaded.

<img class="alignnone size-medium wp-image-3300" src="http://dostmuhammad.com/wp-content/uploads/2015/05/400390_1826119910849_565876858_n-300x160.jpg" alt="400390_1826119910849_565876858_n" />

We have to navigate to this place and find the .hex file. We can copy it to any preferable location and load it in our previously made Proteus schematic of Arduino. If we don’t copy it and save elsewhere it may get lost

<a href="http://dostmuhammad.com/wp-content/uploads/2015/05/424955_1826120470863_386550022_n.jpg"><img class="alignnone size-medium wp-image-3301" src="http://dostmuhammad.com/wp-content/uploads/2015/05/424955_1826120470863_386550022_n-300x159.jpg" alt="424955_1826120470863_386550022_n" /></a>
<div id="fbPhotoSnowboxCaption">Once it is loaded and the simulation is run we can see it is working fine.</div>
<div><img class="alignnone size-medium wp-image-3302" src="http://dostmuhammad.com/wp-content/uploads/2015/05/405495_1826120830872_733664937_n1-300x109.jpg" alt="405495_1826120830872_733664937_n" /></div>
<div>

I hope it will be useful for all Arduino lovers and thereby bring a new era in Arduinoing.

</div>
</section><a href="http://dostmuhammad.com/wp-content/uploads/2015/05/Arduino-Proteus-Simulation-Templates.rar">Arduino Proteus Simulation Templates</a> provided by Shawon Shahryar