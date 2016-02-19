---
layout: post

title: Arduino easiness!
subtitle: "An update on the Arduino drivers"
cover_image: NextDev35.jpg

excerpt: "Yesterday I posted an update to Kickstarter with the news that the libarary and driver for the NextDev was complete.  A number of you asked me for a code example."

author:
  name: Guy Molinari
  #twitter: wckoehler
  bio: Software Engineer, Architect, Hardware Enthusiast
  image: logo.png
---
Yesterday I posted an update to Kickstarter with the news that the libarary and driver for the NextDev was complete.  A number of you asked me for a code example.

{% highlight c++ linenos %}

#include "NextDev.h"

NextDev disp;

void setup() {
  Serial.begin(9600);
  disp.begin();
  Serial.print("Current page = ");
  Serial.println(disp.getPage());
  Serial.print("Screen brightness = ");
  Serial.println(disp.getIntVariable("dim"));
}

void loop() {

    if (disp.available()) {
       Event e = disp.getEvent();
       String v = "b";
       v.concat(e.getComponent() - 1);
       v.concat(".txt");
  
       Serial.println("Value for " + v + " = " + disp.getStringVariable(v));
    }
   
}

{% endhighlight %}


So, imagine you have designed a UI that looks like this via the Nextion editor:
<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>
The Nextion allows you to assign names to each of the components on a page (in fact, the page itself can have a textual name).  In this example I named the button components "b1", "b2", "b3" and "b4".  I set the text values to be "Relay1" through 4.  This is all using the Nextion editor app on my windows desktop.  Then I saved the .HMI file and clicked "Compile".  The editor compiled my UI and generated a ".TFT" file.  I then uploaded this to my display. 
It's not sexy but it shows the "nuts and bolts" behind the example (I'm going to use fancy cropped images in a "real" app).  Then I fired up my Auduino editor on my Mac and wrote the sketch above and flashed it to my NextDev board (connected by a simple USB cable).  Then I clicked "Serial Monitor" on the "Tools" tab.  It showed the following output:

{% highlight c++ %}
Current page = 0
Screen brightness = 100
{% endhighlight %}
Then I clicked each of the buttons (1-4) on the display and got the following:
{% highlight c++ %}
Current page = 0
Screen brightness = 100
Value for b0.txt = Relay 1
Value for b1.txt = Relay 2
Value for b2.txt = Relay 3
Value for b3.txt = Relay 4
{% endhighlight %}
Of course, I need to trigger some sort of action like send a message over WiFi to turn appliances on/off.  I have a "Sonoff" WiFi enabled power switch coming in the mail from iTead.  For a whopping $5!

More coming soon!
Guy



