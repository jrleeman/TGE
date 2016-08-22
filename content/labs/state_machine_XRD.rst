.. _state_machine_XRD:

Building an XRD State Machine
=============================

.. raw:: html

    <div style="margin-top:10px;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/-xrdd8wqYgc" frameborder="0" allowfullscreen>
    </iframe>
    </div>

X-ray diffraction is a commonly used laboratory technique to study the
properties of crystals or determine the makeup of a bulk sample. The video above
summarizes the operation of a diffractometer and shows one in operation. An
X-ray diffractometer emits X-ray radiation towards the sample at a known angle
:math:`\theta`. The radiation is elastically scattered off atoms in the crystalline
lattice. The angle of reflection is equal to the angle of incidence. The
reflected radiation is counted by a detector. By sweeping the emitter and
detector through a range of angles. we will see peaks in the X-ray spectra
characteristic of the material present. Since crystals have regular structures,
at certain incidence angles, the reflections from two adjacent layers
constructively interfere and create a larger radiation count. In this activity,
you will design a simple state machine to control an X-ray diffractometer.

.. figure:: ./images/bragg_diffraction.png
   :align: center
   :scale: 65 %

   `Bragg Diffraction (Wikipedia) <https://commons.wikimedia.org/wiki/File:Bragg_diffraction_2.svg>`_

We often use user stories to define how a machine should operate. The user story
describes the process that the user or technician will go through to use the
machine.

User Story
----------
The user approaches the machine in the off condition. The main power is turned
on and the machine starts with the X-ray source off in the X-ray shutter closed.
The technician opens the safety doors and inserts a sample for analysis. The
doors are closed and the technician sets the scan parameters in the control
software. The software specifies the minimum and maximum angles at which to
scan, the step at which to go between these angles, and how long the radiation
should be counted at each angle. Once the start scan button is clicked, the
machine must verify that the safety doors are closed and the safety interlock
switches are closed. The X-ray shutter is then opened and the X-ray source
turned on. The machine moves to its minimum scanning angle and begins to count
the radiation for the specified time. After this time, the machine moves by the
specified step amount and counts radiation again for the same amount of time.
This process is repeated until the maximum scan angle is reached. If at anytime
during the operation of the machine the safety interlock switch is open, the
machine must immediately turn off the X-ray source, close the X-ray shutter, and
go to the shutdown state. When the scan completes successfully, the machine must
turn off the X-ray source, close the X-ray shutter, and go to the shutdown state
as well.

Assignment
----------
Using what we've learned in class about state machines and state machine
diagrams, draw a state machine diagram that describes the operation of the X-ray
diffractometer. Remember to specify start and end points, error sources, and
keep the number of states reasonable.
