.. _amplifier_activity:

Amplifier Activity
==================

.. figure:: ./images/amplifier_activity.png
   :align: right
   :scale: 35 %

This activity builds on the :ref:`strain_gage_activity` we did earlier. You saw
that the signal from the strain gages was very small, probably only several
millivolts on most setups. A signal that small is hard to measure well,
especially with your Arduino since it only has a 10-bit analog to digital
converter. Now you will use an instrumentation amplifier to amplify the output
of your Wheatstone bridge circuit and be able to measure the signal on the
Arduino.

Materials
---------
* Strain gaged object from the :ref:`strain_gage_activity`
* 0.1uF Ceramic Capacitor x 2 (`Digikey 99-9870-1-ND <http://www.digikey.com/product-detail/en/kemet/C320C104K5R5TA7301/399-9870-1-ND/3726092>`_)
* INA128 instrumentation amplifier (`Digikey INA128PA-ND <http://www.digikey.com/product-detail/en/texas-instruments/INA128PA/INA128PA-ND/300996>`_)
* Gain Resistor 100 :math:`\Omega` 1% (`Digikey RNF14FTD100RCT-ND <http://www.digikey.com/product-detail/en/stackpole-electronics-inc/RNF14FTD100R/RNF14FTD100RCT-ND/1974980>`_)
* Gain Resistor 249 :math:`\Omega` 1% (`Digikey RNF14FTD249RCT-ND <http://www.digikey.com/product-detail/en/stackpole-electronics-inc/RNF14FTD249R/RNF14FTD249RCT-ND/1974990>`_)
* Gain Resistor 511 :math:`\Omega` 1% (`Digikey RNF14FTD511RCT-ND <http://www.digikey.com/product-detail/en/stackpole-electronics-inc/RNF14FTD511R/RNF14FTD511RCT-ND/1975006>`_)
* Arduino Uno
* Hookup Wires
* Potentiometer



Questions/Tasks
---------------
1. Determine what the total change in voltage you expect for your stain gaged
   object is. This could mean squeezing it, compressing it, whatever you designed
   it to measure. How did you do this? What is the expected range? What is the
   DC offset at no load? (6 pts.)

   |

2. Look at the INA128 datasheet carefully. What are the gains set by each of the
   three gain resistors provided? (3 pts.)

   :download:`INA128 Datasheet <ina128.pdf>`

   |

3. What gain is appropriate for your setup to allow the Arduino to measure strains
   on your object? How much of the dynamic range of the ADC do you expect to use?
   (4 pts.)

   |

4. Hookup the instrumentation amplifier of your breadboard as shown below. Use
   the appropriate gain resistor as determined in question three. (0 pts.)

   |

5. Create a sketch to read the ADC on the Arduino and display the ADC counts
   and voltage. Submit your code with the assignment (2 pts.)

   |

6. Connect the differential inputs of the instrumentation amplifier together.
   What is the measured output of the instrumentation amplifier? What would you
   expect it to be? (4 pts.)

   |

7. Given the DC bias of your strain gaged object, will amplification make the
   output of the instrumentation amplifier out of range? (i.e. Would the output
   be higher than the maximum output voltage we can achieve with this circuit?)
   (2 pts.)

   |

8. If you need to offset the inputs to your circuit, use the simple DC-bias
   circuit below. Hookup the Wheatstone bridge to your instrumentation amplifier
   and Arduino. (0 pts.)

   |

9. Collect data from your circuit and make a plot of the time-series of voltage
   as you impose strain to the object. (2 pts.)

   |

10. Devise a way to roughly calibrate your object to measure what you had
    intended. Perform this calibration and present the calibration curve,
    calibration factor, and any potential sources of error. (6 pts.)

|

11. What improvements could we make to this circuit to reduce noise or otherwise
    improve performance? (1 pt.)

Bonus
-----
These are optional bonus questions that require significant amounts of effort,
but will help you gain insight into how strain gage systems and strain gage
load cells work.

12. Assume that one orientation of your gages are fixed value dummy gages. Using
    the gage factor of your gages and your knowledge of Wheatstone bridges,
    calculate the best estimate of strain on your object in the direction of
    the active gages. Show all work. State all assumptions. (6 pts.)

   |

13. We know that the "dummy" gages will deform slightly due to Poisson effects
    as the material is deformed. Calculate the predicted response of your object
    to force taking this into account. What is the predicted calibration factor?
    How does that compare to your measured calibration? (8 pts.)

Grading Rubric
--------------

============================== ==========
Description                    Max Points
============================== ==========
Files named appropriately      5
Questions                      30
Total                          35
============================== ==========
