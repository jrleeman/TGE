.. _arduino_setup:

Getting Started with Arduino
****************************

.. figure:: ./images/icon_arduino_setup.jpg
   :align: right
   :scale: 80 %

We'll be using the Arduino platform to explore basic electronics and
microcontrollers. In this lesson we will learn the basics parts of the Arduino,
install the necessary software to program it, and upload a basic program.

Materials
=========
* Arduino Uno or equivalent
* USB cable (connector depends on Arduino model)
* Computer

Arduino Basics
==============
The Arduino is a small microcontroller that allows you to write firmware to read
sensors, turn things on and off, and make decisions based on those
inputs/outputs. You can think of the Arduino as a small computer, except it has
no operating system. We write some code, translate it to instructions the
Arduino can understand (compiling), and then we upload those instructions to the
memory on the Arduino. While all of the details behind each of those steps are
very interesting, they are a little beyond what we want to accomplish right now.

The `Arduino Uno <https://www.arduino.cc/en/Main/ArduinoBoardUno>`_ itself is
based around an `Atmel <http://www.atmel.com>`_ AVR microcontroller called the
`ATmega328P <http://www.atmel.com/devices/atmega328p.aspx>`_. There is actually
no official designation of what AVR stands for, but it is generally thought to
stand for **A**\ lf (Egil Bogen) and **V**\ egard (Wollan)'s **R**\ ISC
processor. This is an 8-bit processor based on a modified `Harvard Architecture
<https://en.wikipedia.org/wiki/Harvard_architecture>`_ and
`RISC <https://en.wikipedia.org/wiki/Reduced_instruction_set_computing>`_ design.
Knowing what all of those words mean is not essential to getting started, but
worth reading about for those of you that are curious. Arduino is a brand of
products designed with the idea that non-engineers should be able to create
projects that use digital electronics. The `history of the company
<https://en.wikipedia.org/wiki/Arduino#History>`_ starts officially in 2005,
with many changes, conflicts, and all of the normal things experienced by young
technology companies. Arduino was quickly adopted by everyone from artists that
wanted to make colorful and interactive displays to citizen scientists that
wanted to measure their world. Now you see why we are using it for this course.

Learning how to program microcontrollers can be a daunting task. The
`datasheet <http://www.atmel.com/Images/Atmel-42735-8-bit-AVR-Microcontroller-ATmega328-328P_datasheet.pdf>`_
for this very simple processor is a whopping 444 pages, but is the ultimate
source of information. For our projects, we will be using the Arduino
programming environment that makes the native functions of the processor much
easier to use for beginners. It does take a bit of a mental shift if you are
used to programming on personal computers, the Arduino has only 32kB of program
memory space! Working in such resource constrained environments offers many
opportunities to make low power systems, but does require some getting used to.

Take your Arduino out of the packaging and examine it closely. Identifying all
of the parts is not too important right now, but let's take a tour of the
capability of the development board and see where we will connect different
peripherals.

Digital Input/Output
====================
Sometimes called General Purpose Input/Output (GPIO) pins, there are 14 of these
on the Uno. They can serve as an output providing a digital on (5V) or off (0V)
to manipulate attached devices (think of it like a computer controlled light
switch), or as an input that can read if the input is on or off. A few of these
pins have special functions that you may need to be conscious of when designing
a circuit around them:

* Pins 0-1 are for serial receive and transmit respectively. These are connected to a chip that interfaces your Arduino to the USB port and your computer. It's how you program the Arduino and read back data on the serial terminal. Connecting things to these can keep the Arduino from programming properly. Stay away from hooking to these until you're out of pins to use. Then you'll have to unhook them to upload new firmware.
* Pins 2-3 are capable of generating interrupts. This means they can watch their state, and create an event in your code when the state meets certain criteria. For example, you could use an interrupt based on if a pin value changes to count how many times a tipping bucket rain gauge has tipped, since each tip will cause the pin to change state.
* Pins 3,5,6,9,10,11 can generate a Pulse Width Modulated (PWM) waveform. This is used to create an analog voltage output, meaning a voltage that can be anywhere in the voltage range of the processor (0-5V). The PWM modules on the Arduino are 8-bit meaning there are 256 levels of possible votlage output.
* Pins 10-13 can interface to sensors that communicate using the Serial Peripheral Interface (SPI). This is a digital communication protocol often used to connect sensors such as pressure, temperature, and humidity to the microcontroller.
* Pin 13 has an attached light emitting diode (LED) on the circuit board. This is handy for troubleshooting as it requires no external parts.
* SCL/SDA are special purpose pins that communicate with sensors on the Inter-Integrated Circuit protocol (I2C). I2C only requires 2 data wires and is often used for sensors such as pressure, temperature, and humidity.

Analog Input
============
Analog inputs are used to measure a voltage. The Uno has 6 of them labeled
A0-A5. The hardware that does the work of turning a voltage into a digital
representation is called an analog-to-digital converter (ADC). In this case the
ADC is built into the ATmega328P and has 10-bits of resolution. This means the
voltage will be digitized to one of 1024 different values. Be default the input
range is 0-5 VDC, but that can be changed by providing a reference voltage to
the AREF pin.

Power
-----
The Uno has several power "rails" exposed. These can be used to power sensors
and LEDs. If your project has significant power requirements, they may not be
able to provide enough power, but they will provide plenty of power for the
experiments we will be performing.

* Vin connects to the input voltage you provide if using the external power jack. You can also power the Arduino through this pin (7-12 VDC).
* GND connects to the system ground.
* 5V provides regulated 5 VDC power.
* 3.3V provides regulated 3.3 VDC power. Maximum current is 50 mA, so be careful!
* IOREF provides the operating voltage reference for inputs and outputs. This is useful when designing circuits to work with Arduinos of different operating voltages (5 or 3.3VDC).

Other Technical Specifications
==============================

=============================  ========
Specification                   Value
=============================  ========
Recommended Input Voltage      7-12 VDC
DC current per I/O pin         20 mA
DC current for 3.3V power pin  50 mA
Flash memory                   32 kB
SRAM                           2 kB
EEPROM                         1 kB
Clock Speed                    16 MHz
=============================  ========

Installing the Arduino IDE
==========================
We will use the Arduino interactive development environment (IDE) to write our
code, compile, and upload it to the Arduino. This is a free tool that is
actively maintained by the open-source community. It is available for Mac,
Windows, and Linux machines from the `Arduino Software page
<https://www.arduino.cc/en/Main/Software>`_.

Download and install the software as you would any other application on your
machine. Each project will need to be stored in a directory (folder) named the
same thing as the project. It is recommended to store all of these projects in
the "Arduino" directory, created in your documents folder after installing the
IDE.

Your First Program
==================
In the software world, we often write a "Hello, World!" program. In the hardware
world, we often make "blinky", an application that blinks an LED. While that may
not seem very exciting, remember that that LED could represent a pump, light,
fan, linear actuator, or any number of other actuators you can control.

* Open the Arduino IDE and create a new sketch by selecting File > New File, if one was not created when you opened the application.

With the new file open, you will notice it is not empty. The skeleton of an
Arduino has already been populated for you.

.. code-block:: c

    void setup() {
      // put your setup code here, to run once:

    }

    void loop() {
      // put your main code here, to run repeatedly:

    }

The skeleton has two functions, setup and loop. The setup function will run once
when the Arduino is powered on or reset, then the loop function will run. Once
the loop function reaches the end of its instructions, it starts again from the
top. This function will run indefinitely for as along as the microcontroller has
power. We will dive more into what functions mean later, but for now it is time
to get something blinking!

Add the following code to your empty project and save the project as
:code:`my_first_blinky`.

.. code-block:: c

    void setup() {
      // initialize digital pin 13 as an output
      // remember pin 13 already has an LED connected!
      pinMode(13, OUTPUT);
    }

    void loop() {
      // put your main code here, to run repeatedly:
      digitalWrite(13, HIGH);   // turn the LED on
      delay(500);               // wait for 500 ms
      digitalWrite(13, LOW);    // turn the LED off
      delay(500);               // wait for 500 ms
    }

Plug your Arduino into your computer. In the Tools > Board menu select
Arduino/Genuino Uno. Then select the appropriate serial port from the Tools >
Port menu. If you don't know which port to select, try unplugging the board,
then note what options are in the menu. Plug the board back in and the new
option in the menu will be the port the Arduino is on.

Next, press the arrow shaped "Upload" button at the top of the Arduino IDE. Your
program will be compiled and uploaded to the Arduino in a few seconds. If you
look at the Arduino, you should see an LED blinking. Congratulations! You did
it!

This is a pretty simple program that is well commented, but we will quickly go
over how it works. The first thing that happens is the :code:`setup()` function
runs. Everything with :code:`//` before it is a comment and there for human
readability only, the compiler throws all of that away before uploading the
program to the Arduino. The only instruction is :code:`pinMode(13, OUTPUT);`.
Every statement in C (yes, you're really writing C/C++) needs to be completed
with a semicolon. This particular command tells the microprocessor that we are
going to be using pin 13 as an output. The pin is configured and will hold its
status as an output until we change it. The command :code:`digitalWrite` is used
to change the output state of a digital pin. The syntax uses the pin number we
want to modify and the state (high or low) that we wish to assign it. The
:code:`delay` command pauses the execution of the program for the given number
of milliseconds (1 ms = 1/1000 second). In our case we turn the LED on by making
pin 13 high, then waiting 0.5 seconds, then we turn the LED off by making the
pin low, waiting another 0.5 seconds, then the whole thing repeats!

There you have it, your Arduino is setup and you have successfully controlled a
small part of the world. You can keep exploring by checking out the examples in
the File > Examples menu. Examples are one of the best ways to learn, and the
included examples are thoroughly commented. Go through a few, even if you just
read them, to get used to reading the code.
