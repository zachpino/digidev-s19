# Week 07 · Moving Forward 

Let's get things moving today, and learn about power isolation.

- [Components](#components): Motors, Transistors, Diodes, Servos
- [Circuits](#circuits): Motor Control with Distributed Power
- [Code](#code): Transitor Driving and Servo Libary
- [Homework](#homework) : Project Proposal

-----

### Components

#### DC Motor

![DC Motor](https://cdn-shop.adafruit.com/970x728/711-06.jpg)

A DC motor converts electricity into a magnetic field, which in turn drives rotational movement. Inside the motor housing, a set of permanent magnets exert force on the 'armature', a carefully shaped piece of wire through which electrons flow. The magnets exert a force on the electrons as they pass through the cylinder of the motor, and torque is created according to Fleming's [Left Hand Rule](https://en.wikipedia.org/wiki/Fleming%27s_left-hand_rule_for_motors). DC motors are designed to spin fast, and not to exert much torque. For this reason, they often require [gearing up or down](https://en.wikipedia.org/wiki/Gear).

Motors are simple components, but they require a couple of safety measures [explained well here](http://www.sharetechnote.com/html/Arduino_MotorBasics.html). Rather than driving motors directly with a PWM pin, it is very important to use a transistor with a PWM pin as well as a diode to protect the Arduino.

Fancy motor driving chips, like the well-known [L293D](https://www.adafruit.com/product/807), can toggle the polarity of the signal and allow a DC motor to spin in both directions. With a transistor, though, only one direction of spin is possible.

Motors require electricity to spin, but they can also be spun to *produce electricity*. When used in this way, DC motors are instead called turbines, and are deployed all over the world as [hydroelecric and anemoelectric generators](https://en.wikipedia.org/wiki/Water_turbine). This allows for fun power storage and reclamation projects [like this one](https://www.wired.com/story/battery-built-from-concrete/).

![motor working principle](http://hyperphysics.phy-astr.gsu.edu/hbase/magnetic/imgmag/dcmcur.gif)


#### NPN Transistor

![NPN Transistor](https://cdn-shop.adafruit.com/970x728/756-03.jpg)

Transistors sit at the heart of every general purpose computer, making up the processors of computers. Transistors are fundamentally switches — but rather than relying upon a human for actuation — an electric current is used to open a connection. Whatever is connected to the *collector* leg is released to the *emitter* leg when the *base leg* receives power above a certain threshold. Read that last sentence a few times, and it will make sense!

![transistor legs](https://www.elprocus.com/wp-content/uploads/2013/01/NPN.jpg)

Transistors are often used to manipulate high voltage and amperage electrical components with low voltage controllers and drivers.


#### Diode

![diodes](https://cdn-shop.adafruit.com/970x728/755-03.jpg)

Diodes are simple components. They are wires, but they only allow the flow of electricity in one direction. In most cases, diodes are used as *flybacks*, which [protect components from high kickback voltage](https://en.wikipedia.org/wiki/Flyback_diode). Diodes always have a stripe or mark on them near their *cathode*. Electrons can only flow through diodes from anode to cathode, so commonly in circuits, it looks like they are connected backwards — since they are there for protection! [All LEDs are diodes](https://learn.sparkfun.com/tutorials/polarity/diode-and-led-polarity), it just so happens that they convert electons flowing through them into visual photos, rather than heat.


#### (Micro)Servo Motor

![Micro Servo](https://cdn-shop.adafruit.com/970x728/169-06.jpg)

Servo motors are DC motors with a reducing [gear train](https://en.wikipedia.org/wiki/Gear_train) inside as well as a control board. Depending on the length of pulses received on a signal wire, the servo motor will turn to a specific degree. This motion takes time, and so it is important to add `delay()`s to your code to provide time for the movement to complete. Servos are essential for most robotics and controlled motion applications. Microservos, like the ones included in our kits, are normally limited to a bit less than 180 degrees of motion. 'Continous Rotation' servos allow for full 360 degree motion.

![exploded servo](https://upload.wikimedia.org/wikipedia/commons/e/ec/Exploded_Servo.jpg)

----- 

### Circuits

Remember to try to wire with an encoding schema in mind...

- Red for 5V Power
- Orange for 3V3 Power
- Black, White, Gray, or Brown for Ground
- Yellow or Purple for Generic Signals
- Green and Blue for I2C Communication

#### Motor Control with Distributed Power

Let's protect our Arduino with a diode and transistor, and tap into an alternate power supply. Additionally, let's control a servo motor for precise motion.

![motors](motors.png)

-----

### Code

Double check that "Tools" -> "Board" is set to "Arduino/Genuino Uno" and that "Tools" -> "Port" is set to whichever "COM" USB port has a connected "Arduino Uno".

#### Transitor Driving and Servo Libary

```c
int motorPin = 3;
 
void setup() 
{ 
  pinMode(motorPin, OUTPUT);
  Serial.begin(9600);
} 
 
 
void loop() 
{ 
  if (Serial.available())
  {
    int motorSpeed = Serial.parseInt();
    if ((motorSpeed >= 0) && (motorSpeed <= 255))
    {
      analogWrite(motorPin, motorSpeed);
    }
  }
} 

```

-----

### Homework

Formal project time! 

Please prepare a short presentation (10 slides), and include the following:

- Motivation statement / Problem to solve
- Audience definition
- Set of technologies you'd like to explore
- Some sketches of possible outcomes
- List of functionalities you'd like to support in hardware and in software
- Comparable / Inspirational projects
