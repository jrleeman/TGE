.. _madara_ben_2016:

Strain Gauge Based Displacement Measurement - Ben Madara
========================================================

**Problem:**

There are several displacement measurement methods. Currently, I utilize
a linear variable differential transformer to measure the compaction and
dilation of my experimental samples under load. This LVDT is housed
inside of a high pressure vessel. LVDT is quite large for a crowded
space as it requires two additional steel blocks to be fit into the set
up. Additionally, the necessity of the steel mounting blocks means the
measurement is not directly on the sample. This means the displacement
measured is also dependent on any tilting of the mounting and loading
blocks.

**Solution:**

I built a strain gauge based system to measure the horizontal
displacement. The design was a prototype to be used outside of the
pressure vessel that fits onto the 10x10 blocks in the biax. The larger
size was for simplicity of electrical connection and the use of already
owned strain gauges. The system works by measuring the change in
resistance between four strain gauges laid out in a diamond shape by
means of a Wheatstone bridge. The base material for the diamond shape
bracket needs an elastic yield point higher than 30 MPa, so I used an
aluminum alloy (McMaster-Carr 5052). The bracket frame was designed in
Onshape. The design was first 3d printed to ensure sizing and
functionality of the parts. Then a water just was used to cut the
bracket pieces out of a ¼” aluminum plate. Once the pieces were in hand
I was able to apply the four strain gauges, one to each of the aluminum
bracket pieces. With the strain gauges super glued in place the
connections were then soldered to complete a Wheatstone bridge. By using
an external power source and multimeter the bracket was then bench
tested. Upon a successful bench test the Wheatstone bridge was then
connected to an amplifier circuit built on an Arduino Uno. The signal
was amplified by the Texas Instruments INA128 amplifier. The Arduino was
programmed to print and plot the voltage coming out of the Wheatstone
bridge. The prototype successfully recorded strain and fit onto the
10x10 blocks for use in the biax. For future development of this project
the first step would be to get higher quality strain gauges.
Additionally, another amplifier and filtering of the data would improve
the signal to noise ratio in the measurements.

Media
-----
:download:`Slides (PDF) <madara_presentation.pdf>`

:download:`Slides (PPTX) <madara_presentation.pptx>`

.. raw:: html

  <div style="margin-top:10px;">
  <iframe width="560" height="315" src="https://www.youtube.com/embed/694oz7dl5MQ" frameborder="0" allowfullscreen>
  </iframe>
  </div>
