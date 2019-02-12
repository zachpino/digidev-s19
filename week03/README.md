# Week 03 · Looping Beats

We've so far written code that runs from top to bottom. *Check a sensor*, *do some math*, *send out a signal*. We've looked at branching with `if(){}` and `else{}` as a way to allow code to make a decision, but our code has never before iterated or looped through a set of repeatable commands, or remained in a certain state until something changed. Let's make that happen today and massively increase our programming power.

We may also explore function declarations for reusable code, depending on timing.

We'll look at music as a space to explore controlled looping. Please check out [this wikipedia page](https://en.wikipedia.org/wiki/Piano_key_frequencies) as a reference for the frequency parameter of musical notes.

- [Hydraulic Analogy for Electricity](https://learn.sparkfun.com/tutorials/voltage-current-resistance-and-ohms-law/current)
- [Components](#components): Passive or Active Piezo Buzzer
- [Circuits](#circuits): Keyboard and Drum Machine
- [Code](#code): tone(), for(){}, while(){}, delayMicroseconds()
- [Homework](#homework) : Light-Theremin

-----

### Components

#### Passive Piezo Buzzer

![RGB LED](https://cdn-shop.adafruit.com/970x728/1536-06.jpg)

*Piezo* is a prefix and standalone term that comes up frequently in electronics. It always refers to how materials that assume a crystalline structure like minerals and ceramics can store electric charges, and when they do, oscillate and vibrate at very predictable rates. This works in both directions — a small crystal will vibrate at a certain frequency when a current of a certain voltage is passed through it, and if one vibrates that same small crystal at that same frequency, it will produce identical voltage. For this reason, piezo crystal oscillators (often called 'quartz' oscillators) are used in just about any computational system to keep accurate time.

A piezo buzzer leverages this physical phenomenon and uses *oscillating* electrical signals to vibrate a small crystal, which in turn displaces a certain amount of air. This displacement creates a vacuum, and a [sound wave](https://en.wikipedia.org/wiki/Sound#Sound_wave_properties_and_characteristics) is formed. [Beep!](https://www.youtube.com/watch?v=AhrtsxbZvok) 

Piezo buzzers create monophonic waves with little possible expressibility. Notably, with additional coding work, other [shapes of sound waves](https://en.wikipedia.org/wiki/Square_wave) than regular square waves can be made that approximate more natural sounds. They will always sound like old cellphone ringtones: buzzes, beeps, and bloops. [Clever coding and fancy wiring](http://www.opencircuits.com/Microcontroller_polyphony) can produce [simple polyphony](https://en.wikipedia.org/wiki/Polyphony), but piezo buzzers will never sound like a violin or a saxophone. 

Note that Passive Piezo Buzzers require a PWM pin to operate, as a quickly oscillating electrical signal is required.


#### Active Piezo Buzzer

![Active vs Passive](https://www.sunfounder.com/media/wysiwyg/swatches/sensor_kit_v2_0_for_arduino/22_buzzer_module/20150902162620.png)

Active buzzer, with black epoxy on bottom, at left. Passive buzzer, with green PCB, at right. 

Active buzzers are fancier than passive buzzers, but operate on the same principle. An electric current is passed through a crystal, causing a small but very fast vibration — which in turn creates an air pressure wave. An active buzzer has a current oscillator built into it, so all that is required is applied voltage to make sound (no PWM pin necessary). A constant `HIGH` signal will make sound, no `LOW` pulsing is required. There's very little reason to choose a more expensive and complicated Active Buzzer over a Passive Buzzer, unless you are totally out of PWM pins.


#### Trimpots and Potentiometers

![Trimpot](https://cdn.sparkfun.com//assets/parts/3/8/2/3/09806-01.jpg)

Potentiometers, and their tiny family members trimpots, are resistors - though their resistance is not set and instead changes depending on the position of a knob. As the knob is rotated clockwise, a conductive wiper inside moves along a resistive strip, forcing the electrons to travel through more or less resistive material. This attenuates the electrical signal, weakening it proportionally.

![conductive wiper](https://i.stack.imgur.com/XXQEm.gif)

----- 

### Circuits

Remember to try to wire with an encoding schema in mind...

- Red for 5V Power
- Orange for 3V3 Power
- Black, White, Gray, or Brown for Ground
- Yellow or Purple for Generic Signals
- Green and Blue for I2C Communication

But, since we are using so many buttons this week, we can vary our sensor wire colors for clarity. Always choose wire colors for understandability, even if it means violating the above guidelines! 

#### Keyboard and Drum Machine

Let's make some noise.

![keyboard and drum machine](keyboard.png)

Let's control that noise?

![keyboard and drum machine](keyboard_volume.png)

-----

### Code

Double check that "Tools" -> "Board" is set to "Arduino/Genuino Uno" and that "Tools" -> "Port" is set to whichever "COM" USB port has a connected "Arduino Uno".

```c
int potPin = A0;
int buzzerPin = 6;


void setup() {
  // put your setup code here, to run once:
  pinMode(potPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  
}

void loop() {
  // put your main code here, to run repeatedly:

  int potValue = analogRead(potPin);

  int mappedValue = map(potValue, 0, 1023, 110, 1568);
  
  tone(buzzerPin, mappedValue);

}
```

-----

### Homework

Download and explore [Fritzing](http://fritzing.org).

Create a photoresistor-based [theremin](https://en.wikipedia.org/wiki/Theremin). Allow the musician to control notes, rhythm, and/or volume with buttons or trimpots.

For inspiration, you also may want to check out [this documentary on Robert Moog](https://www.youtube.com/watch?v=XRg8R-00mjs) and the birth of electronic music, a woefully underappreciated design and technology revolution that directly paved the way to *fundamentally new sounds* for the human species, and led to the character of nearly all music produced today.

Create your circuit and behavior, and then use Fritzing to produce a diagram of your work.