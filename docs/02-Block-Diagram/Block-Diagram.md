---
title: Arm System Block Diagram
tags:
- tag1
- tag2
---

## Arm System Block Diagram
![](block_diagram.png)

### Block diagram decision making process
* The robot arm is intended to have 4 joints, as shown in Fig. 16 on the team concept design page linked [here](https://egr314-s-2026-303.github.io/02-Concept-Design/Design/). Only one joint needs to have more than 180 degrees of rotation, the base joint that rotates the entire arm, and needs to be serially controlled as per class requirements. Thus, there is one stepper motor controlled by the TMC2209 stepper driver and three servo motors controlled by PWM signals.
* In order to control the robot arm, it must communicate with the HMI and WiFi interfaces, which are managed by [Lia's board](https://lryan5.github.io/) and [Matthew's board](https://msande84.github.io/msande84.EGR314.github.io/) respectively, thus UART1 is reserved for this. Although UART1 and UART2 are assigned to GPIO pins in the final design, I decided to show them as separate blocks in the ESP32 block to show that it is separate from the PWM pins.
* UART2 is reserved for communicating via single-wire UART to the TMC2209.
* The USB port is also a separate block to show that the ESP32 is programmable.
* The 3.3V switching power supply does not directly power the servos and the stepper motor and controller, but specific pins on these devices use 3.3V from a microcontroller, thus the area governed by the power supply overlap those components halfway. The 5V and 12V sources supply the bulk power the servos and stepper motor respectively.
* The 12V source can also be a 9V source if using the specific 3A power supply provided in class, which was done many times for debugging, so there is the option provided in the block diagram for bulk power.

### How block diagram meets requirements
The block diagram meets the requirements by including:
1. a 3.3V switching regulator;
2. the esp32 which is intended to be surface mount;
3. UART communication interface for WiFi board and HMI to control robot arm, thus wireless control and HMI control is present;
4. all the joint actuators required for a robot arm to pick up objects and flip over the robot, all permitted due to one being a stepper motor and the servos being extra to class requirements;
5. a battery to provide 12V to the 3.3V switching regulator.