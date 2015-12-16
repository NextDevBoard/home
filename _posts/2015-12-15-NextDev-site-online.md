---
layout: post

title: Introducing NextDev!
subtitle: "A User Interface for the IoT"
cover_image: nextdev-back.jpg

excerpt: "NextDev is a small, low cost, WiFi (Internet) connected device designed to integrate with a LCD TFT touch screen display.    In a very real sense it is a standalone computer for controlling a network of sensors and actuators.   It simplifies the development your own applications for the Internet of Things (IoT)."

author:
  name: Guy Molinari
  #twitter: wckoehler
  bio: Software Engineer, Architect, Hardware Enthusiast
  image: logo.png
---
NextDev is a small, low cost, WiFi (Internet) connected device designed to integrate with a LCD TFT touch screen display.    In a very real sense it is a standalone computer for controlling a network of sensors and actuators.   It simplifies the development your own applications for the Internet of Things (IoT). Constructing a user interface UI can be a challenging and time consuming endeavor.

> “NextDev makes this process fun!"

NextDev integrates two technology components:

* The ESP8266 WiFi System on a Chip (SoC).  This has taken the maker community by a storm.
* The Nextion TFT display from ITead Studio, a company who will also be the manufacturing partner for the NextDev.

NextDev utilizes your choice of existing software development platforms:

* The LUA scripting language via NodeMCU.
* The Arduino IDE tool for the ESP8622.
* Native ESP8266 SDK.

NextDev interoperates and interconnects with other IoT platforms via standard communication protocols such as MQTT.

#How NextDev Works

I'll show you how this process works using the relay demo shown in the KickStarer video as a use case.

Here are the steps to build an application:

## Step 1 - Layout your UI using the Nextion Editor.
You can download the Nextion editor from THIS LINK.  Add 4 button components to the first page of your UI.  In my case I just used simple buttons.   If desired, you can associate these with images that you upload to the Nextion display's flash storage.  When you are done generate a .TFT file and copy it to a micro SD card.  And plug it into the Nextion.  It will be transferred to the Nextions internal flash.  Power it down and remove the SD card.  You are ready to control this UI from NextDev.

<!-- Image of Nextion Editor with 4 button UI -->
<!--<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>-->

## Step 2 - Write your code and upload it to NextDev.
For this example I will use the LUA scripting language.  Code can also be written using the Arduino IDE for the ESP8266.  By default, the LUA runtime environment (NodeMCU) and the NextDev driver APIs are shipped pre-installed on the NextDev.  

The first thing you need to do is initialize the library and Nextion display.  Then send a command to tell the display to go to the first page.  It is possible to divide the UI into multiple pages (and for smaller LCD panels is almost a necessity).

Here is the sample code:

{% highlight lua linenos %}
disp = require("Nextion")
disp.init()

disp.onSysErr(function(err)
    print("Error code = " .. err)  -- If an error occurs, print the details to the debug console.
end)

-- This API call registers a function that will be called whenever a touch event occurs!
disp.onTouchEvent(function(page, comp, evt)
    print("Page " .. page .. " Component " .. comp .. " Event " .. evt)
    -- Your code goes here
end)

disp.sendCommand("page 0") -- If this command is not specified, the display will start with the first page.

{% endhighlight %}

Transfer this code to your NextDev board via a USB cable.  There are a number of IDE tools available for the NodeMCU firmware.  My favorite is ESPlorer.  You can download this software here:  ESPLORER LINK.



## Step 3 - Configure the WiFi connection on the NextDev.
Go to a web browser and connext type in **192.168.4.4**.  The following web page will be displayed:

<!-- Image of web page with NextDev config web page ->>
<!--<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>-->

Enter the configuration settings for your router (SSID, password) and the IP address of an MQTT broker.  You can use our broker or you can set up your own if desired.   We are using the open source broker called **mosquitto** (www.mosquitto.org).  Click **Save** and power cycle the NextDev.   

You are good to go!


##Additional Uses

The NextDev board alone (without Nextion display) can be used to add WiFi connectivity to your Raspberry Pi!


##Zoomable images

Image of the frong of NextDev

<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>

That's all for now. Thanks for reading.
