---
layout: post

title: Arduino easiness!
subtitle: "An update on the Ardino drivers"
cover_image: nextdev35.jpg

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
       Event* e = disp.getEvent();
       String v = "b";
       v.concat(e->getComponent() - 1);
       v.concat(".txt");
       delete e;
  
       Serial.println("Value for " + v + " = " + disp.getStringVariable(v));
    }
   
}

{% endhighlight %}


So, imagine you have designed a UI that looks like this via the Nextion editor.
<div class="full zoomable"><img src="{{ site.baseurl }}/images/nextdev-front.jpg"></div>

