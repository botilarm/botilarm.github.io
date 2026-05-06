---
title: Hardware V2.0
---

## Overview
This page is dedicated to describing the top 5 improvements to version 1.0 of the hardware design to be implemented in version 2.0, listed from most important to least important.

>Note: some of the changes below to hardware have been implemented in the second version of the PCB design, shown [here](https://botilarm.github.io/06-PCB/pcb/).

## Improvement 1: Using a stepper driver IC that is more hand-solderable
The main failure of the design was the stepper driver; the SMD board mounted stepper driver circuit was unfortunately never able to function, therefore, as you can see in the [PCB page](https://botilarm.github.io/06-PCB/pcb/) in the populated ver. 1, a breakout version of the TMC2209 was mounted to a perf board and connected to the extra IO pins of the ESP32 to get it functional.

In version 2.0, it would be better to use a stepper driver in a package that has all SMD pins further spaced apart and accessible from the top so continuity can be accurately determined, such as in a SOP or QFP. The QFN package in 1.0 is difficult to debug without special equipment.

## Improvement 2: Correct pushbutton footprints and Include BOOT button
These two improvements have been merged into one due to them both being related to the pushbuttons in the design. 

The first major issue was the fact that the pushbutton footprints made it so the buttons were always shorted; this required the buttons to be rotated and not connected to all 4 pins of the DPST switch when assembling.

The second issue was that there was no button connected to the BOOT pin (IO0) on the ESP32, causing it to never be able to enter programming mode. This was fixed in assembly by adding another pushbutton to a perf board and soldering it to the IO0 pin on the esp32, which was frustrating.

In version 2.0 there should be correct footprints and an actual switch on the BOOT button for these reasons.

## Improvement 3: Extra pin headers for power rails
The initial design had no way to connect a component not mounted on the PCB to any of the power rails unless you piggybacked off of an existing pin. This had to be done to get the PCB working, but it was very frustrating. Therefore, in version 2.0 there should be extra ground and extra 3.3V, 5V, and 12V pins to attach components not originally onto the PCB.

## Improvement 4: Test points
Test points are a simple through hole component mounted to the PCB to allow you to use a multimeter to test voltage or continuity from one point to another. In the initial design, there were no dedicated test points for any of the power rails. In version 2, there should at least be test points on each rail at least.



>**Note:** the extra 12V supply pins should not be connected to generic ~1mm 2.54mm pitch pin headers, as this could melt the header and it is easy to accidentally short the pin header to something you don't want it to short to. Thus in 2.0 the extra 12V supply should be via a terminal block.

## Improvement 5: Fuse for 12V power rail
Although the 12V supply rail did not ever cause catastrophic issues due to not having a fuse, it would be best to include one in the next design.