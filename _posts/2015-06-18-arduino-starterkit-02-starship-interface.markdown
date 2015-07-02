---
layout:     post
title:      "The Arduino Starter Kit - 02 Starship Interface"
date:       2015-06-18 23:41:00
category: programming
tags: [arduino, arduino-starter-kit]
---

{% include gallery.html %}

Continuing with the [Arduino Starter Kit](http://www.arduino.cc/en/Main/ArduinoStarterKit) series, the second project - [Spaceship Interface](http://www.arduino.cc/en/ArduinoStarterKit/Prj02) - is the first project to include code next to the actual circuit:  
{% highlight c %}  
// Create a global variable to hold the
// state of the switch. This variable is persistent
// throughout the program. Whenever you refer to
// switchState, you’re talking about the number it holds
int switchstate = 0;

void setup() {
  // declare the LED pins as outputs
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);

  // declare the switch pin as an input
  pinMode(2, INPUT);
}

void loop() {
  // read the value of the switch
  // digitalRead() checks to see if there is voltage
  // on the pin or not
  switchstate = digitalRead(2);

  // if the button is not pressed
  // turn on the green LED and off the red LEDs  
  if (switchstate == LOW) {
    digitalWrite(3, HIGH); // turn the green LED on pin 3 on
    digitalWrite(4, LOW);  // turn the red LED on pin 4 off
    digitalWrite(5, LOW);  // turn the red LED on pin 5 off
  }
  // this else is part of the above if() statement.
  // if the switch is not LOW (the button is pressed)
  // turn off the green LED and blink alternatively the red LEDs 
  else {
    digitalWrite(3, LOW);  // turn the green LED on pin 3 off
    digitalWrite(4, LOW);  // turn the red LED on pin 4 off
    digitalWrite(5, HIGH); // turn the red LED on pin 5 on
    // wait for a quarter second before changing the light
    delay(250);
    digitalWrite(4, HIGH); // turn the red LED on pin 4 on
    digitalWrite(5, LOW);  // turn the red LED on pin 5 off
    // wait for a quarter second before changing the light
    delay(250);
  }
}
{% endhighlight %}

The program is uploaded onto the Arduino Uno board making two red LEDs alternatively turn on and off while a push button is kept pressed. Initially, when this switch is not pushed, there's a third green LED that is on. When the swith is pushed the green LED turns off. At the same time the two other red LEDs start switching on and off every quarter of a second - simulating a spaceship command panel (just like at the board of the [Star Trek](http://www.imdb.com/title/tt0060028/episodes?season=1&ref_=tt_eps_sn_1) Enterprise). There is also a paper cover to use in order to hide the circuit and make the board look closer to a spaceship console.

`Three covered LEDs while the push button is switched off`  
<a href="/assets/images/arduino-starterkit-02-three-leds-covered-switch-off.jpg" data-lightbox="gallery" title="Three covered LEDs while the switch is not pressed">
    <img src="/assets/images/thumbs/arduino-starterkit-02-three-leds-covered-switch-off.jpg" alt="Three covered LEDs - push button switched off" />
</a>

`Three covered LEDs while the push button is kept switched on`  
<a href="/assets/images/arduino-starterkit-02-three-leds-covered-switch-on.jpg" data-lightbox="gallery" title="Three covered LEDs while the switch is pressed">
    <img src="/assets/images/thumbs/arduino-starterkit-02-three-leds-covered-switch-on.jpg" alt="Three covered LEDs - push button switched on" />
</a>

`Three LEDs with no cover`  
<a href="/assets/images/arduino-starterkit-02-three-leds-no-cover.jpg" data-lightbox="gallery" title="Three LEDs with no cover">
    <img src="/assets/images/thumbs/arduino-starterkit-02-three-leds-no-cover.jpg" alt="Three LEDs with no cover" />
</a>

`Four LEDs with no cover while the push button is switched off`  
<a href="/assets/images/arduino-starterkit-02-four-leds-no-cover-switch-off.jpg" data-lightbox="gallery" title="Four LEDs with no cover while the switch is not pressed">
    <img src="/assets/images/thumbs/arduino-starterkit-02-four-leds-no-cover-switch-off.jpg" alt="Four LEDs with no cover - push button switched off" />
</a>

`Four LEDs with no cover while the push button is kept switched on`
{% raw %}
<video preload="metadata" controls="controls">
  <source src="/assets/videos/arduino-starterkit-02-four-leds-no-cover-swith-on.mp4" type="video/mp4">
  Four LEDs with no cover - push button switched on
</video>
{% endraw %}
