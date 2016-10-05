.. _bending_forces:

Bending Forces
==============

.. figure:: ./images/plate_bending.gif
   :align: right
   :scale: 100 %

   Image: `Efunda <http://www.efunda.com/formulae/solid_mechanics/plates/calculators/cpS_PUniform.cfm#Results>`_.

This page shows the way to calculate the bending force and displacement on a
circular plate that is simply supported and loaded uniformly. This is a useful
calculation to perform for end platens on internal pressure vessels.

Plate Rigidity
--------------
:math:`D = \frac{E t^3}{12(1-\nu)}`

Displacement
------------
:math:`y_c = \frac{-qa^4}{64D} \frac{5+\nu}{1+\nu}`

Stress
------

:math:`M_\text{max} = \frac{qa^2}{16}(3+\nu)`

:math:`\sigma_\text{max} = M_\text{max} \frac{6}{t^2}`

Nomenclature
------------
* :math:`D` = Plate rigidity
* :math:`q` = Load/area
* :math:`a` = Radius of plate
* :math:`t` = Thickness
* :math:`E` = Young's modulus
* :math:`\nu` = Poisson's ratio
* :math:`y` = Displacement
* :math:`M` = Moment
* :math:`\sigma` = Stress
