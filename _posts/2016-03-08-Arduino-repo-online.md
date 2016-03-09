---
layout: post

title: Arduino repository online.
subtitle: "The Arduino repo is available for preview."
cover_image: NextDev35.jpg

excerpt: "Over the past few days I have started to get the Arduino code repository online so that the community can get a preview."

author:
  name: Guy Molinari
  #twitter: wckoehler
  bio: Software Engineer, Architect, Hardware Enthusiast
  image: logo.png
---
I have been pondering how I might distribute the Arduino software stack for NextDev.   The initial thought is that I would just release the code in the form of libraries that could be installed
individually.   Then I thought, why not fork the repo at esp8266.com and create my own board manager.   This way all a developer needs to do is set up the URL to the board manager file location 
and then click install.   All of the necessary bits would be installed right into the IDE in one click of a mouse button.  Of course, none of this is terribly useful without the NextDev board in
hand.  But then I thought why not get this done and out of the way while I am dealing with the day to day details of getting the manufacturing deliverables done and coordinating the various aspects
of this project.  It is exhausing but I want to make sure the community can jump right in when the boards arrive.   One of the goals of the NextDev project is really to build a community around
this endeavour.   I would much rather this be a collaborative effort and look forward to the involvement of the larger community.  

Another possibility is thorough testing using non-NextDev boards that are based upon the ESP-12 module such as NodeMCU 0.9.  The SPI-to-UART bridge will not work of course, but other boards would 
at least provide access to schetches that use core WiFi capbility.  If nothing else, it would confirm that the board manager will install correctly.

Another aspect of this is the release of the repository for code review and inspection.   Many pair of eyes can be helpful in spotting problems early and addressing functionality gaps.  I have added 
two new libraries.

* *SpiSerial* - This library provides an API for interfacing with the SC16IS750 SPI/UART bridge device.  This is a dependency of the NextDev library and is not directly accessed by the developer.
* *NextDev* - This library provides an API for all NextDev functionality including the 8 additional GPIO pins.

Some additional libraries were also included in the repository:

* *QueueList* - This library is a dependency of the NextDev API and is used for event queuing.
* *ArduinoJson* - This library not a dependency of NextDev but is included as a convenience for building IoT applications.
* *PubSubClient* - This library is also not a dependency of NextDev but again included as a convenience for building IoT applications.

Please let me know if there are any other "must haves" and I will include them.   Also, please don't be shy and submit a pull request.  Just fork the repo and hack away.

## Repository location
`http://github.com/NextDevBoard/Arduino`

## Installation instructions

* You must be running version 1.6.6 (or later) of the Arduino IDE.  You can download or upgrade by accessing the `arduino.cc` site.
* You’ll need to point the Arduino IDE board manager to a custom URL. Open up Arduino, then go to the Preferences (*File* > *Preferences*). Then, towards the bottom of the window, paste this URL into the “Additional Board Manager URLs” text box: `https://raw.githubusercontent.com/NextDevBoard/Arduino/master/install/package_nextdev_index.json`.  Then click OK to save the change.
* Then navigate to the Board Manager by going to *Tools* > *Boards* > *Boards Manager*. Look for esp8266. Click on that entry, then select Install.

After a few minutes the all files will be installed and ready for use.  A few more configuration steps to configure your board:

* With the Board addon installed, all that’s left to do is select “NextDev 1.0 (ESP-12 Module)” from the *Tools* > *Boards* menu.
* Connect your board using a short USB cable.  Actually shorter is better for higher transfer speeds.
* Then select your FTDI’s port number under the *Tools* > *Port* menu.  The baud rate defaults to 115200.  This is quite slow.  Try selecting 921600 for blazing fast flash updates.

You are now ready to write your first sketch.  You can find some examples on the *Sketchbook* menu.

Next step is to bring the NodeMCU/Lua repo online and get feedback there as well.


More coming soon!
Guy



