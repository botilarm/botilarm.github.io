---
title: Reflection
---

## Overview
This page describes the success of the module, lessons learned, tips/recommendations for future students of EGR314: Embedded Systems Design II.

## Module's Success
The module was a success in the sense that all components present on the board functioned and completed necessary verification assignments. It did not, however, include all extra functionality to fulfill the requirements of the project. It is missing three servo motors which are the other three joints of the robot arm. It is also missing the structure and claw mechanism and associated inverse kinematics.

Initially, the intended message structure for the robot arm would include an X, Y, and Z coordinate that the arm would attempt to move to, but this was replaced with simple stepper motor control as that is all the functionality that was achieved by the end of the project.

Thus, the requirement that the arm can collect and deposit samples and that it can flip over the robot are missing.

## Microcontroller/Module Startup Tips
1. Include the necessary pushbuttons for allowing the microcontroller to enter programming mode. For the ESP32, this means a pullup switch on the EN and BOOT pins, EN (pin 3) and IO0 (pin 27) respectively.
2. If using solder paste for the microcontroller and IC components in general, make sure that the solder has a good connection between the pad of the PCB and the pad of the IC. When testing continuity between pins, put the multimeter probe on the very top of the IC pins so that you verify that the IC is actually connected to the pad below.
3. Use Thonny with ESP32 for the easiest coding experience, and do not use the generic ESP32-S3 firmware for every ESP32 microcontroller; try to find the exact name of the esp32 you are using when selecting firmware to flash.

## Lessons Learned
These are the top 10 most important things learned from working on this project.
1. The smaller the component, the harder it is to verify whether it is connected correctly or not.
2. The PCB will most likely not work as intended; having test points and the ability to expand the PCB is essential for getting it to work in a timely manner.
3. The due dates for assignments should be followed because it is easy to fall behind.
4. Team communication is key to getting a working system.
5. Clearly labeled pins on the silkscreen layer make PCB assembly much easier.
6. Not every component needs to be bought.
7. Debugging AI code is never as worth it as writing the code yourself.
8. Circuit protection is essential.
9. The professors and TAs have been through similar experiences and can oftentimes recognize issues faster than you can.
10. Through hole components are much easier to manually solder than SMD.

## Recommendations for future students
These are the top 5 recommendations to prepare future students taking Embedded Systems II:
1. Fail early; this means getting your design done and tested as early as possible so that all problems can be discovered before you are struggling to solve a basic problem that is a struggle because you are having to edit a manufactured PCB.
2. Although an objective in PCB design is to have things be as small as possible; we're still learning about these components, so don't overreduce the size of your design. Find surface mount components that can still be easily hand soldered and debugged. Only rely on solder paste for basic components that can easily be debugged, such as resistors, switches, and LEDs.
3. Try to make your project fulfill requirements in the simplest way possible. Most of the class is spent debugging, so the more complexity you add to your project, the more time you will spend debugging as more components have the chance to not work.
4. Disconnect power from boards when connecting them for verification; also do not rush connecting the team in a daisy chain. Depending on the state of everyone's module, wires may change colors or pins change meaning. Double check that you are connecting everything correct; components will break and have to be replaced if the utmost care is not exercised.
5. Try to actually scout for teammates that you think you will work well with. Much of your grade is dependent on team assignments and team functionality, so ensure they will be as committed as you.