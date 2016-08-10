.. _blinky_1.0:

Blinky 1.0
==========

This activity will get you familiar with the Arduino programming environment
and show you how to blink an on-board LED with a simple program that we will
write, compile, and upload.

Materials
---------
* Arduino UNO
* USB Cable
* Computer (Mac, Linux, Windows)

Installing the Arduino IDE
--------------------------
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
------------------
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
