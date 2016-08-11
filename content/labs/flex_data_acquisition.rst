.. _flex_data_acquisition:

Flex Sensor Data Acquisition
============================

.. figure:: ./images/icon_flex_sensor.png
   :align: right
   :scale: 70%

In this activity you will learn how to take a transducer, create a basic signal
conditioning circuit, then record data from that system. We will be using the
flex sensor from the Inventor's Kit and measure how far you have bent the sensor
over time. This could represent the bending of a structure in the wind or the
deformation of a system in laboratory. These sensors have also been used in
virtual reality/game sensor systems and in the construction of robots.  We will
go through each step of the data acquisition process to build a system to record
the approximate angle of bend of the sensor.

Materials
---------
* Arduino UNO
* USB Cable
* Breadboard
* M/M Jumper wires
* Flex Sensor
* 47k :math:`\Omega` resistors (Yellow-Violet-Orange)
* Computer (Mac, Linux, Windows)

Sensor
------------
The flex sensors in the activity are made by SpectraSymbol
(checkout the `datasheet <https://cdn.sparkfun.com/datasheets/Sensors/ForceFlex/FLEX%20SENSOR%20DATA%20SHEET%202014.pdf>`_ ).
They are coated on one side with a polymer that has little conductive bits in it. When
the sensor is flat (unbent), the characteristic resistance is about 30k :math:`\Omega` .

.. figure:: ./images/flex_sensor_straight.png
   :align: center
   :scale: 80%

   `Straight flex sensor (Image: Sparkfun) <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview>`_

When you bend the sensor, the same number of conductive bits are stretched over a longer
distance, making the resistance increase to about 70k :math:`\Omega` at a 90 degree bend.
We can verify this with a multimeter.

.. figure:: ./images/flex_sensor_bent.png
   :align: center
   :scale: 80%

   `Bent flex sensor (Image: Sparkfun) <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview>`_

Do **NOT** kink the sensor near the base or bend it in the wrong direction! This can
damage it. It should only be bent as shown in the photo below.


.. figure:: ./images/flex_sensor_direction.png
   :align: center
   :scale: 40%

   `Only bend the sensor in this direction (Image: Sparkfun) <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview>`_

The most recent shipment of sensors seem to be slightly different than the
specifications used in the SparkFun tutorial materials. The unbent resistance
is about 22k :math:`\Omega` and at ninety degrees bend it is about
48k :math:`\Omega`.

Signal Conditioning
-------------------

You have probably noticed that the Arduino doesn't have a port to plug in a
sensor and measure its resistance. We need to condition the signal to be
something that our acquisition hardware can handle. We are going to take a very
simple approach here and use only a voltage divider circuit. This is a common
technique that we will see again.

A voltage divider consists of two resistors in series. If we put a voltage
:math:`V_\text{in}` at the top of the series resistor string and ground the
other end, the output at the junction of the two resistors will be:

.. figure:: ./images/resistor_divider.png
   :align: left
   :scale: 120%

   `Simple voltage divider (Image: Wikipedia) <https://commons.wikimedia.org/wiki/File:Resistive_divider2.svg>`_


.. math::
   V_\text{out} = V_\text{in} \frac{R_2}{R_1+R_2}


We will implement the resistor divider by making :math:`R_1` in the circuit
above be the flex sensor. As it flexes, the resistance will increase. This
increase in :math:`R_1` will make the output voltage of the circuit go down
towards ground. Ideally there would be a buffer circuit in between the voltage
divider and the acquisition system, but for this particular setup and
application it is not necessary. The voltage divider is designed to give us a
wide range of output voltages, but some other sensors with smaller changes
in resistance (such as strain gauges) would need amplification in addition to
buffering. That's coming in another activity though. We can represent our
system with the schematic below.

.. figure:: ./images/flex_sensor_schematic.png
   :align: center
   :scale: 60%

   `Flex sensor schematic (Image: Sparkfun) <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview>`_


ADC/Firmware
------------
Now that we have a conditioned signal that represents the physical thing we are
trying to measure, it is time to turn those voltages into a digital
representation that we can record. We will use the on-board analog-to-digital
converter to read the voltage and convert it to a value the computer can record.
The process behind this will be discussed in a future class.

The Arduino's ADC can read voltages from 0-5 VDC with a 10-bit resolution,
meaning that we can resolve 1024 different values. That's plenty for what we
are trying to do here. Let's have a look at the firmware that's going to
run in this exercise.

.. code-block:: c

  /*********************************************************************************
  Modified from the SparkFun Flex Sensor Example Code
  https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview
  **********************************************************************************/

  const int FLEX_PIN = A0; // Pin connected to voltage divider output

  // Measure the voltage at 5V and the actual resistance of your
  // 47k resistor, and enter them below. This makes the angle
  // calculation much more accurate.
  const float VCC = 4.8; // Measured voltage of Arduino 5V line
  const float R_DIV = 45900.0; // Measured resistance of 47k resistor

  // Upload the code and try to determine an average value of
  // resistance when the sensor is not bent, and when it is
  // bent at 90 degrees. Enter those and reload the code for
  // a more accurate angle estimate.
  const float STRAIGHT_RESISTANCE = 22250.51; // resistance when straight
  const float BEND_RESISTANCE = 48300.0; // resistance at 90 deg

  void setup()
  {
    Serial.begin(9600); // Startup the serial communications at 9600 baud
  }

  void loop()
  {
    // Read the ADC
    int flexADC = analogRead(FLEX_PIN);

    // Calculate the voltage that the ADC read
    float flexV = flexADC * VCC / 1023.0;

    // Calculate the resistance of the flex sensor
    float flexR = R_DIV * (VCC / flexV - 1.0);


    // Use the calculated resistance to estimate the sensor's
    // bend angle my mapping the measured resistance onto the
    // known resistances at zero and ninety degrees of bend.
    float angle = map(flexR, STRAIGHT_RESISTANCE, BEND_RESISTANCE,
                     0, 90.0);

    // Send the results back to the computer formatted as a
    // comma delimited line.
    Serial.print(angle);
    Serial.print(",");
    Serial.println(flexR);

    delay(250); // Read the sensor at 4Hz.
  }

The :code:`setup()` function starts serial communication with the computer.
In the main :code:`loop()` function we read the ADC value with the
:code:`analogRead()` command and convert it to an actual voltage. Don't worry
too much about that yet. We next convert that voltage to a resistance of the
flex sensor by doing a bit of algebra on the voltage divider equation above
to solve for :math:`R_1`:

.. math::
   R_1 = R_2 \frac{V_\text{in} - V_\text{out}}{V_\text{out}}

which can be written a bit more nicely as:

.. math::
   R_1 = R_2 \left(\frac{V_\text{in}}{V_\text{out}} - 1 \right)

We then use the :code:`map()` function which is a handy way to avoid doing the
annoying math of scaling and calibration in this case. We assume the sensor
is linear and map takes our no bend and bent resistance values and maps them
to zero and ninety degrees. It then takes the measured resistance and estimates
the bend angle based on those two end point calibration values. Checkout the
`documentation for the map function <https://www.arduino.cc/en/Reference/Map>`_
for the details.

Logging
-------
Now that we have the Arduino reading the sensor and converting that digital
value back into a meaningful physical unit, we need to record that data. Often
in the lab this means writing custom software, but for our simple needs we can
use the tools built into the Arduino IDE.

The serial monitor tool (magnifying glass icon) will show the serial traffic
that the Arduino is sending back to us. You can copy and paste the data from
there into a text editor and save it, but there is a limited row number history.
You can pull this data into your favorite graphing tool of choice to make a
plot.

If you go into the tools menu of the IDE, there is a Serial Plotter option.
Clicking that will show a running graph of the serial data coming in, but it is
rather limited. There is no time scale and there can only be one plot running.
To use the serial plotter we need to change the serial output section of the
code to output only a single angle value per line, no comma or resistance.
After you get your calibration resistances (see below) you can modify the
serial section to just be :code:`Serial.println(angle);` (just commenting out
the other lines is a good idea).

For a good summary of the current state of the serial plotter, checkout this
`blog post <https://rheingoldheavy.com/new-arduino-serial-plotter/>`_ by
Rheingold Heavy.

If you have problems with either of these methods, check that the baud rate
of the terminal/plotter is set to 9600. You can also use an external serial
monitor like `CoolTerm <http://freeware.the-meiers.org>`_ that will log directly
to a file and has many other bells and whistles.

Procedure
---------

* Connect your flex sensor to the Arduino as shown in the diagram below.

.. figure:: ./images/flex_sensor_fritzing.png
  :align: center
  :scale: 30%

  `Flex sensor hookup diagram (Image: Sparkfun) <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide#flex-sensor-overview>`_

* Plug the Arduino into the computer and upload the program listed above.

* Experiment with the plotter and sensor. Try changing the resistor in the
  voltage divider out for one of higher or lower value. How does the output
  voltage change? Does the range of output voltage change?

Deliverables
------------
Turn in a plot of the bend of your sensor over time as you manipulate it. This
can be a plot from the Arduino IDE or one you make in your favorite graphing
software.

Images from the `Sparkfun Flex Tutorial <https://learn.sparkfun.com/tutorials/flex-sensor-hookup-guide>`_
are licensed under `CC BY-NC-SA 3.0 <http://creativecommons.org/licenses/by-nc-sa/3.0/>`_ .
