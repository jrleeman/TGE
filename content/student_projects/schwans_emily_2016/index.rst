.. _schwans_emily_2016:

Lightweight Precision Altimeter for UAV Survey of Ice - Emily Schwans
=====================================================================

**Problem Statement**

Determining the location of the ice-air interface relative to the flight height
of a UAV within the order of magnitude of accuracy needed for a high resolution,
low frequency GPR survey is difficult to do using a simple DGPS altimeter,
especially when working in a temperate area where there is likely to be a wet
interface on the surface of the glacier that will cause a large amount of
scatter of EM energy. Verification of interfaces within ice detected with GPR
without digging pits or doing other ground-based work is also difficult. Hence,
developing a low-cost, lightweight solution for accurate altimetry measurements
is one of the first steps in designing a system for testing the feasibility of
sounding en- and subglacial hydrologic systems in temperate glaciers using low
frequency, drone- based GPR.

**Design Considerations**

While laser or ultrasonic rangefinders are more accurate than pressure-based
altimeters, the former are expensive for far-ranges. Using a pressure sensor
that resolves output to within fractions of a Pascal is accurate enough for
this stage of design, and cost-effective in terms of the parts I needed. The
hypothetical UAV-mounted GPR system would have to be light; therefore the
altimeter has to be lightweight also. Additionally, the antenna on that system
could not be heavy, either, so it would likely be necessary to use SAR
techniques to increase the aperture of the antenna while keeping the desired
low frequency and a small/light antenna. To do this, as precise of location
data as possible are needed during flight time, including altitude
measurements. This is why I chose a sensor that is accurate to within 30 cm
(even down to 6 cm, according to the data sheet), weighs very little, and is
compact. Another design consideration was the need to take readings at a rate
suitable for a potential UAV-based GPR survey (Rückamp et. al. 2011 cite 10Hz
as their sampling rate for a UAS-based GPR survey). The sensor I used can
output data at a comparable rate. The sensor is also effective down to -40 ̊C,
so it would be usable in a cold setting.

**Implementation Process**

Testing and prototyping was done with Arduino Redboard, requiring no soldering.
While I did initially attempt to solder wires to the sensor so I could have it
off the breadboard and do the rest of the circuitry with plenty of room to work
with, I discovered I am not at all skilled in through-hole soldering. So, after
ruining the first sensor I got and having to reorder another on my own, I
decided to simply use the breadboard. This worked nicely, allowing me to rework
my circuit as needed: adding buttons to switch modes was much easier. In
hindsight, I would have liked to have learned how to solder better early on so
that when this project rolled around, I’d be better prepared and could have
produced a more compact, less wire-intensive prototype.

The sensor itself was quite simple to hook up using the breadboard and jumper
cables. However, it required an input of 3.3V, and to communicate with it using
5V RedBoard, I had to add in-line resistors to the SCL and SDL connections,
despite powering it directly with the 3.3V output on the Redboard. Initially, I
simply had it plugged into the breadboard with jumper wires, but it kept
slipping around and losing contact with the resistors, giving me a -999.99
reading for everything. So, I bent jumper wires and resistors to maintain
contact. However, maintaining contact between the resistors and the breadboard
for the button was a big issue while I was testing my code. In hindsight,
getting a smaller board that I could physically solder components to would have
been prudent, assuming I could have done clean soldering work.

Using a MacBook Air to upload the code was a big challenge: often, it would not
recognize that my board was connected, so most of the time I was unable to
upload the code without restarting my computer, and using the Serial Monitor or
Plotter to get arrays of data was more or less impossible.

Additionally, I attempted to use a 7-segment LED display with pins on both
sides, but was unable to get it to display what I wanted with enough detail to
be useful. I found that the LCD display included in my inventor’s kit was much
easier to use once I figured out how to connect all the pins, and was much
better to read data off of and to see when I switched between modes. It also
didn’t take up as much room on my breadboard having only one side with pins,
which was nice since I had to also add a potentiometer to adjust the contrast on
the LCD display so I could read it. Had I known the LED would take up most of
the breadboard, I would not have gotten that part. Also, I failed to take into
account that this display would not have enough digits for readings in Pascals
at the level of accuracy I desired.

For my code, I spent quite a while figuring out how to convert the reading from
20-bit to an actual altitude/pressure reading. This initial code was very long
and took up a lot of memory on my RedBoard, which had been temperamental since
the beginning, but even more so when the code took up more memory. Luckily, in
going over the data sheets and specs online, I realized that there were
libraries for my sensor out there that did the same thing I was trying to do,
but in a much more simple way that took up less memory on my RedBoard when used.
I looked into the source files for those libraries to make sure I wasn’t just
relying on a black box, but ultimately used these libraries instead of writing
everything from scratch, because “reinventing the wheel”, so to speak, is not
time-effective, and using code that comes with a part you use seems reasonable
as long as you understand how it works.

In general, I programmed the Arduino as a state machine; it continually takes
readings in altitude mode until I press the button and switch states between
either two altimetry modes (meters and feet above sea level) or one barometric
mode, plus an initial state to configure the sensor, and a shutdown state, which
it switches to when outside the operating temperature range. I could have also
had additional states for changing between Pascals, mmHg, or millibars, but this
was not part of my original design and theoretically I’d be using the data as an
array anyhow, so could easily convert this post-acquisition.

I did not have the time to figure out how to hook up the battery to power the
altimeter, but can do so in the future. I also could not figure out how to set
the user-input sea level pressure, which is why the instrument is not very
precise.

**Instrument Testing**

Accuracy in the altitude readings was tested by comparing altitude in multiple
locations to those shown on topographic maps. Pressure readings were compared to
local weather website measurements. Temperatures were compared to multiple
thermostats. Ultimately, the temperature readings were accurate, as were the
pressure readings, but the altitude drifted a lot. To get an idea of instrument
drift, I carried the prototype up and down the stairwell, making note of any
differences I saw in the top and bottom measurements over the course of carrying
it up and down several times. At times, it was off by several meters.

**Next Steps**

A more permanent, compact design could be achieved using an Arduino Pro Mini
($9.95), which weighs less than 2 grams, has the same number of I/O pins, 2
extra analog pins compared to Redboard, and features an off-board USB
connection. This would require more soldering work, but is necessary for a more
refined prototype. Attaching the battery and the on/off switch, as well as
adding a

Standby mode to conserve battery power while measurements are not being taken
would be helpful. A chassis to protect the electronics from weather would also
be a step in producing a more permanent product for field implementation.
Additionally, programming the board in such a way so that it can either store
measurements or transmit data via WiFi or Bluetooth to a computer or phone is
necessary for field implementation, the latter of which is likely more realistic
given the scope of a UAV-based survey and the amount of memory typically
available.

The instrument doesn’t “settle down” to the point where altitude is not
constantly changing. This is a design flaw, and would have to be fixed if this
were to be implemented for high-precision measurements while flying. This is due
to the fact that the device is using pressure (which is varying) to calculate
altitude. Having an insulated chassis could help with this.

**Summary**

All in all, I succeeded in designing a prototype for a high-accuracy
pressure/altitude sensor that, with some tweaks and downsizing, could be used
for UAV acquisition, albeit a laser range finder would be the best permanent
solution (albeit expensive). I would need to fix the drift in the instrument and
program a smaller, more permanent Arduino that could be attached to the sensor.
I learned that soldering is not as easy as it looks, that circuits are
complicated and I forgot a lot of what I learned about them in physics over the
course of four years, and that, while it is easy to get lost in datasheets,
really reading into the full capabilities of a given sensor is necessary to
obtain the exact results you want.

Media
-----
:download:`Slides (PDF) <schwans_presentation.pdf>`

:download:`Code (ZIP) <schwans_code.zip>`

.. raw:: html

 <div style="margin-top:10px;">
 <iframe width="560" height="315" src="https://www.youtube.com/embed/TApfCxidbRE" frameborder="0" allowfullscreen>
 </iframe>
 </div>
