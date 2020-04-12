# Arduino Speed Log

In this folder you can find files with the program and schematics of the control board for a simple paddlewheel based speed log. You can find the mechanical components for download at Thingiverse:

https://www.thingiverse.com/thing:4279708

The intended use of this design is two-fold: for the one hand showing how these systems work; for the other hand, allowing the use of a simple and inexpensive speed log for small DIY crafts. Although the use of a small size GPS could do much the same with more accuracy, I have developed this for use in a small size low-cost ROV (Remotely Operated Vehicle) for underwater exploration. There, there is no GPS at all.

The working procedure of the speed log is similar to those commercially available for boats ands yachts, but at a smaller scale. The incoming flow of water makes the impeller rotate. Each of the impeller paddles contains a small magnet. A simple electronics board counts each time a magnet passes the top most part. The velocity of the vessel over the water is proportional to the count (in reality it is not proportional, but for the intended use is perfectly fine to assume proportionality).

Components
----------

You need the following electronic components:

- 1 x Arduino UNO
- 1 x Hall effect switch (ML 007-1)
- 1 x 16x2 LCD (1602A)
- 1 x I2C to parallel (LCM 1602). Based on the PCF 8574

Code
----

The code is extremely simple. It loops reading the hall effect sensor, and counts the transitions between 0-1 or 1-0 (no magnet-magnet and magnet-no magnet). Every 250 ms the value of the counter is shown on the LCD and sent through the serial port. The count is porportional to the boat speed by the equation:

boat_speed = K * count

The proportionality constant can be found by using a GPS while keeping the boat at a fixed speed. Let's say that you get actual_count while navigating at gps_speed. Then the constant can be found by:

K = gps_speed / actual_count

