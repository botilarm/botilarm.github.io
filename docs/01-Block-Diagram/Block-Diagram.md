---
title: Individal Block Diagram
tags:
- tag1
- tag2
---

## Overview
The block diagram is a way to clearly lay out each team member's individual project, consisting of one or more analog sensors and/or actuators.

The block diagram below describes a project part of a smart plug that is part of a larger smart power strip that monitors power usage for each appliance plugged in and allows the user to program when each plug is on or off.

In this block diagram there are two power sources, one described as a 120V 20A AC Outlet which is the standard for a home in America. Within the PIC circuit there is a 5V 1.5A Voltage Regulator which can be derivative of the one constructed in class or from a manufacturer, and the purpose of that is to power the logic, pushbuttons, sensors, and other peripherals that aren't part of the appliance being measured.

Combined with an analog reading of current from another team member, this individual project intends to calculate power in watts and over time in kW/h and display it to a 4 bit 7 segment display for monitoring.

## Block Diagram Image
![block_diagram](block_diagram_drawio.png "Block Diagram") <br>
*Armando Botiller's Individual Block Diagram*