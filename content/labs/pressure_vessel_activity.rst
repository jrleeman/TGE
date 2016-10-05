.. _pressure_vessel_activity:

Pressure Vessel Design Activity
===============================

Pressure vessels are everywhere in the experimental lab, from the air compressor
to experimental material deformation and failure test chambers. In this activity
you will perform the calculations we discussed in class to design a simple
pressure vessel that could be used in the laboratory.

When doing your design, use good practice and document your assumptions,
design decision reasoning, and clearly show all calculations. Calculations may
be performed by hand or with a script. If you use a script, please clearly
comment it and include it with your assignment. Python notebooks are ideally
suited to this task as they allow you to combine documentation, photos, etc.
with your code into a complete lab writeup, but you may use any tool you wish.
We strongly encourage you to **NOT** use Microsoft Excel as it is an accounting
and spreadsheet program, not an engineering program and can be very difficult
to debug.

Background
----------
Gas hydrates are a unique material in which molecule(s) of a gas, such as
methane or carbon-dioxide are trapped inside a cage of water molecules. This
solid looks similar to ice, but can have very different properties. Hydrates
(or clathrates as they are sometimes called) are an active area of research
and could be important for the storage of greenhouse gasses and present hazards
to hydrocarbon drilling and exploration operations. Hydrates were even a large
barrier to getting the Deepwater Horizon spill under control. When engineers
attempted to capture the well's output with a metal cage termed the "top-hat
solution", hydrates filled the structure and lifted it off of the well as they
are less dense than water. Hydrates can be important for understanding submarine
slope failure and geologic processes on other planets and moons.

Pressure Vessel Requirements
----------------------------
To investigate some of the properties of gas hydrates, we want to be able to
make some in the laboratory. Since this is a new project, we have no facilities
other than standard laboratory and break-room equipment. We need to design a
pressure vessel that lets us produce some methane hydrate. We can then take the
hydrate out of the vessel and light it on fire (in a controlled environment)
to impress our funding agency and get funding for better equipment.

* Hydrate must be a stable phase when the pressure vessel is placed into the
  laboratory refrigerator, which is stable at 2 :math:`^\circ` C.

* The safety factor must be at least 4 at the maximum expected operating
  pressure of the vessel.

* The vessel will be made of 6061 Aluminum stock.

* Assume that the O-ring sealing is a solved problem for this vessel, no need
  to worry about designing the gland dimensions.

* The vessel will be capped with two flat plates that are bolted onto the end
  of the vessel.

* The vessel inner diameter should be 10 cm.

* The vessel inner length should be 10 cm.

Questions/Design Tasks
----------------------

1. Knowing that the laboratory refrigerator is 2 :math:`^\circ` C, what is the expected
   pressure of the phase boundary from gas + liquid water to gas hydrate? To
   be sure we are completely into the stable field and give our refrigerator
   a little room for error, add 50% to that. What is this design pressure?
   (4 pts.)

   |

2. Let's start by filling our vessel with 500 mL of liquid water, then sealing
   it up. What is the total volume of the vessel? What is the gas headspace of
   the vessel?
   (2 pts.)

   |

3. Stoichiometrically, hydrate is 4CH :math:`_4 \cdot` 23H :math:`_2` O. We want to
   make sure we can completely convert all of the water to hydrate, so we
   make sure that we have 6x as many water molecules as we have gas molecules.
   How many moles of water are in the vessel? How many moles of gas are
   required to complete the reaction?
   (4 pts.)

   |

4. Given the headspace you calculated, how many moles of gas are
   required to keep the pressure at our target at 2 :math:`^\circ` C?
   Is that enough gas? If not, what is the pressure when enough gas is in
   the vessel?
   (6 pts.)

   |

5. When we charge the vessel with gas, we can assume that it is at room
   temperature. As the gas cools in the refrigerator, the pressure will be
   reduced. Given the pressure of the gas you calculated above, what is the
   maximum pressure of the vessel when at room temperature? This will be your
   target design pressure.
   (4 pts.)

   |

6. What is the yield strength, Young's modulus, and Poisson's ratio of 6061
   Aluminum?
   (3 pts.)

   |

7. Calculate the wall thickness required to meet the maximum pressure and
   factor of safety requirements. Round the thickness up to the nearest
   millimeter. You can use a guess and check method, rewrite the equation, or
   work it out with your favorite numerical method.
   (6 pts.)

   |

8. Plot the circumferential stress as a function of radius through the wall
   material. Where is this stress maximized.
   (6 pts.)

   |

9. Calculate the axial stress on the pressure vessel. Is this greater or less
   than the circumferential stress? Does it mean you need to invoke any design
   changes?
   (6 pts.)

   |

10. Calculate the radial stress on the pressure vessel. Is this greater or less
    than the circumferential and axial stresses? Does it mean you need to invoke
    any design changes?
    (6 pts.)

    |

11. Calculate the bending stress on the end platens of the vessel. What is it?
    (6 pts.)

    |

12. Given the factor of safety we desire, what should the thickness of the end
    platens be?
    (6 pts.)

    |

13. Make a plot of the deflection of the end plate at maximum pressure.
    What would be maximum deflection of the end platens be? At what radius is
    it maximized?
    (6 pts.)

    |

14. Assume we are going to use 6 bolts to fix the platen to the end of the
    pressure vessel. How much stress will each bolt need to be able to support?
    Look at the strength of different bolt sizes and grades. What size of grade 8
    hardware should be used to prevent fastener failure?
    (8 pts.)

    |

15. What concerns do you have about this design? What things have we not
    considered or what assumptions that were made in the calculations may not
    be completely valid?
    (5 pts.)

    |

16. What practical/manufacturing constraints could you apply to the design to
    make it cheaper (via reducing the cost of stock metal and/or the machining)?
    Can you do this without impacting the safety of the design?
    (5 pts.)

    |
