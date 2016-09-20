.. _digital_representation:

Digital Representation
======================

Computers communicate with a binary (on/off) logic system. We can represent
numbers in decimal (base 10), hexadecimal (base 8), or pure binary (base 2).
All binary numbers are represented in **big endian** format.

1. Complete the table below with the other two forms of the given number.
   (2 pts. each)

=======  ===========  =========
Decimal  Hexadecimal  Binary
=======  ===========  =========
\        \            0110_0111
\        0x0D
124      \            \
\        \            1111_1111
256      \            \
\        0xDE         \
\        \            1010_1101
190      \            \
\        0xFF         \
\        \            1010_1010
85       \            \
=======  ===========  =========

2. What is the largest decimal value that can be represented by an 8 bit binary
   value? What about 10, 16, and 24 bits? (8 pts.)

|
|
|
|

3. What values (two) in the table above would be easy to use as troubleshooting
   characters when looking at the signal on an oscilloscope or logic analyzer?
   Why? (3 pts.)

|
|
|
|

4. Complete the table below with the unsigned and two's complement value of
   the given binary number. (2 pts. each)

=========  ==============  ================
Binary     Unsigned Value  Two's Complement
=========  ==============  ================
0111_1111
1000_0001
1111_1110
0101_1010
0000_0001
1000_1100
=========  ==============  ================

5. Assume a number is stored in the IEEE 754 single-precision floating point
   representation. The hexadecimal representation of this is 0x40490E56.
   What is the floating point number? (5 pts.)

|
|
|
|

6. Why should floating point calculations be avoided, especially in
   single-precision systems? (5 pts.)

|
|
|
|

7. Describe two ways you could implement a complex equation or operation on a
   resource constrained processor like an Arduino. (6 pts.)

|
|
|
|
