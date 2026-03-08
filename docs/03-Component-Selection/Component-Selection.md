---
title: Module's Selected Major Components
---

## Module's Selected Major Components

The following sections are the selected major components necessary for the arm system.

### Power Management

(**remove this note/placeholder**: this is where your 3.3 volt switching regulator, any other needed power regulator, and power source {if applicable} **THAT WERE SELECTED**)
For more details, review the ["Appendix - Component Selection Process - Power Mangement"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#power-management) selection.

## Module's Considered Major Components
### Primary actuator

*Table 1: Primary actuators component selection*
| **Component**                                                                                                                                                                                     | **Pros**                                                                                                           | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| ![](stepper1.png)<br> SM-42HB34F08AB STEP MOTOR HYBRID BIPOLAR 12VDC<br>$11.84/each<br>[link to product](https://www.digikey.com/en/products/detail/olimex-ltd/SM-42HB34F08AB/21662229)  | \* Inexpensive<br>\* High holding torque 31.15 oz-in easier to implement without gearbox<br> | \* Limited datasheet page|

### Primary actuator controller
| **Component**                                                                                                                                                                                     | **Pros**                                                                                                           | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| ![](controller1.png)<br> A4988SETTR-T IC MTR DRVR BIPOLAR 3-5.5V 28QFN<br>$11.84/each<br>[link to product](https://www.digikey.com/en/products/detail/olimex-ltd/SM-42HB34F08AB/21662229)  | \* Inexpensive<br>\* Lots of documentation to help implement.<br>\* Works within same voltage level as selected ESP32 microcontroller.<br>\* Can control selected bipolar primary actuator with reasonable accuracy. | \* No serial communication options: only logic using 7 wires.|

### Secondary actuators

*Table 2: Secondary actuators component selection*
| **Component**                                                                                                                                                                                      | **Pros**                                                                                                           | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](SERVO1.jpg)<br> SER0056 2KG 300 CLUTCH SERVO<br>$6/each<br>[link to product](https://www.digikey.com/en/products/detail/dfrobot/SER0056/13545236)  | \* Inexpensive<br>\* High torque<br>\*Clutch system and electrical protection prevents damage to motor when motor is blocked from rotating.<br> \* 300 degree range.<br> \* Easy to control with PWM signal.<br>\* Plastic gears make servo lighter, self lubricating, and more vibration dampening.<br>  | \* Cannot meet serial communication for actuator requirement.<br>\* 300 degree range is superfluous for design as only 180 degrees is required.<br>|
| ![](SERVO2.jpg)<br> SER0011 SERVOMOTOR RC 6V MICRO METAL GEAR<br>$8.62/each<br>[link to product](https://www.digikey.com/en/products/detail/dfrobot/SER0011/7087129) | \* Fairly inexpensive<br>\* 2.5 kg torque<br>\* Metal gears less likely to be stripped by softer structural links attached to motor.             | \*Cannot meeet serial communication for actuator requirement.