.. _PID_activity:

PID Controllers
===============

It can take awhile to gain some intuition about control systems, especially
PID controllers. In this activity you will build a simple PID controller with
your Arduino and adjust the different gain settings to see their effects. This
lab is largely based on a lab written by Bret Comnes and A. La Rosa at Portland
State University. Their original lab activity is available on `their website <https://www.pdx.edu/nanogroup/sites/www.pdx.edu.nanogroup/files/2013_Arduino%20PID%20Lab_0.pdf>`_ .

The control system you will build tries to maintain a constant light level on
a photo resistor. You can think of this like your laptop screen that becomes
brighter or dimmer based on the ambient light levels. This is a closed-loop
system since we have a feedback path. An open-loop equivalent would be a
traditional dimmer switch in a room. If the ambient light (sunlight) level
changes, there is no feedback to change the room lights. You must walk over to
the switch and adjust it manually (feed forward control).

In our system, an LED will shine directly into the photo resistor. The setpoint
of the system is adjustable with a potentiometer on the board. The gains of the
controller can be changed using the serial interface.

Materials
---------
* Arduino UNO
* USB Cable
* LED
* 330 :math:`\Omega` resistor (Orange-Orange-Brown)
* 10k :math:`\Omega` resistor (Brown-Black-Orange)
* Photo resistor
* Breadboard
* M/M Jumper wires
* Computer (Mac, Linux, Windows)

Tasks
-----
1. We could write all of the PID control code ourselves, but there is an
   Arduino library available with a very robust controller. Installing the
   library is easy. Download the library zip file from the GitHub repository
   `here <https://github.com/br3ttb/Arduino-PID-Library/archive/master.zip>`_
   or clone into the `repository <https://github.com/br3ttb/Arduino-PID-Library>`_
   if you are comfortable doing that. Unzip the folder and move it to the
   Arduino library folder. In most installations you will find this in your
   Documents folder: *~/Documents/Arduino/libraries*. If your folder
   has hyphens in the name, change them to underscores. If the Arduino IDE was
   open, restart it. You should find new examples for the PID library in
   *File -> Examples -> PID*. Have a look at the examples to get an idea
   of how the library works.

|
|

2. Using the parts in your kit, build the circuit we will use shown below.
   Take a photo of your circuit and attach it to the lab report. (2 pts.)

   .. figure:: ./images/PID_circuit.png
      :align: center
      :scale: 70%

      `Image: pdx.edu <https://www.pdx.edu/nanogroup/sites/www.pdx.edu.nanogroup/files/2013_Arduino%20PID%20Lab_0.pdf>`_

      |
      |

3. Read the following sketch and upload it to your Arduino.

.. code-block:: c

    // From https://github.com/bcomnes/315-lab-microcontroller/blob/master/code/pid_led_set_serial/pid_led_set_serial.ino
    #include <PID_v1.h>
    const int photores = A0; // Photo resistor input
    const int pot = A1; // Potentiometer input
    const int led = 9; // LED output
    double lightLevel; //variable that stores the incoming light level

    // Tuning parameters
    float Kp=0; //Initial Proportional Gain
    float Ki=10; //Initial Integral Gain
    float Kd=0;  //Initial Differential Gain

    double Setpoint, Input, Output;  //These are just variables for storing values
    PID myPID(&Input, &Output, &Setpoint, Kp, Ki, Kd, DIRECT); // This sets up our PDID Loop
    //Input is our PV
    //Output is our u(t)
    //Setpoint is our SP
    const int sampleRate = 1; // Variable that determines how fast our PID loop runs

    // Communication setup
    const long serialPing = 500; //This determines how often we ping our loop
    // Serial pingback interval in milliseconds
    unsigned long now = 0; //This variable is used to keep track of time
    // placehodler for current timestamp
    unsigned long lastMessage = 0; //This keeps track of when our loop last spoke to serial
    // last message timestamp.

    void setup(){
      lightLevel = analogRead(photores); //Read in light level
      Input = map(lightLevel, 0, 1024, 0, 255); //Change read scale to analog out scale
      Setpoint = map(analogRead(pot), 0, 1024, 0, 255);  //get our setpoint from our pot
      Serial.begin(9600); //Start a serial session
      myPID.SetMode(AUTOMATIC);  //Turn on the PID loop
      myPID.SetSampleTime(sampleRate); //Sets the sample rate

      Serial.println("Begin"); // Hello World!
      lastMessage = millis(); // timestamp
    }

    void loop(){
      Setpoint = map(analogRead(pot), 0, 1024, 0, 255); //Read our setpoint
      lightLevel = analogRead(photores); //Get the light level
      Input = map(lightLevel, 0, 900, 0, 255); //Map it to the right scale
      myPID.Compute();  //Run the PID loop
      analogWrite(led, Output);  //Write out the output from the PID loop to our LED pin

      now = millis(); //Keep track of time
      if(now - lastMessage > serialPing) {  //If its been long enough give us some info on serial
        // this should execute less frequently
        // send a message back to the mother ship
        Serial.print("Setpoint = ");
        Serial.print(Setpoint);
        Serial.print(" Input = ");
        Serial.print(Input);
        Serial.print(" Output = ");
        Serial.print(Output);
        Serial.print("\n");
        if (Serial.available() > 0) { //If we sent the program a command deal with it
          for (int x = 0; x < 4; x++) {
            switch (x) {
              case 0:
                Kp = Serial.parseFloat();
                break;
              case 1:
                Ki = Serial.parseFloat();
                break;
              case 2:
                Kd = Serial.parseFloat();
                break;
              case 3:
                for (int y = Serial.available(); y == 0; y--) {
                  Serial.read();  //Clear out any residual junk
                }
                break;
            }
          }
          Serial.print(" Kp,Ki,Kd = ");
          Serial.print(Kp);
          Serial.print(",");
          Serial.print(Ki);
          Serial.print(",");
          Serial.println(Kd);  //Let us know what we just received
          myPID.SetTunings(Kp, Ki, Kd); //Set the PID gain constants and start running
        }

        lastMessage = now;
        //update the time stamp.
      }

    }

4. What are the initial values of the :math:`K_p, K_i, K_d` gains? (3 pts.)

|
|

5. What happens as you change the set point of the system using the
   potentiometer? (2 pts.)

   |
   |

6. At a fixed set point, change the level of incoming light by shielding the
   setup with your hands and by increasing the light level using a flashlight.
   How fast does the system respond? (2 pts.)

   |
   |

7. Using the serial monitor, change the gain settings by sending three numbers
   separated by commas. For example to set :math:`K_p=2, K_i=10, K_d=0` you
   would send ``2,10,0``. Systematically vary the :math:`K_i` setting with both
   :math:`K_p` and :math:`K_d` set to zero. Describe the effect this has. Why
   is it so? (4 pts.)

   |
   |

8. Set :math:`K_i` to 10 and systematically increase :math:`K_p` with :math:`K_d`
   set to zero. Describe the effect this has. Why is this so? (4 pts.)

   |
   |

9. Set :math:`K_i` to 10 and systematically increase :math:`K_d` with :math:`K_p`
   set to zero. Describe the effect this has. Why is this so? (4 pts.)

  |
  |

10. Does this system have any equivalent mass or inertial effects? (2 pts.)

|
|

11. What parameters seem to be the best for controlling the light level? Why do
    you think that is? (2 pts.)

    |
    |
