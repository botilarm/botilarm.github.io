---
title: Module's Selected Major Components
---

## Module's Selected Major Components

The following sections are the selected major components necessary for the arm system.

### Power Management

(**remove this note/placeholder**: this is where your 3.3 volt switching regulator, any other needed power regulator, and power source {if applicable} **THAT WERE SELECTED**)

For more details, review the ["Appendix - Component Selection Process - Power Mangement"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#power-management) selection.


### Actuator

(**remove this note/placeholder**: if applicable, this is where your **Selected** the actuator items go, which includes both the driver and motor. Otherwise, remove this section.)

For more details, review the ["Appendix - Component Selection Process - Actuator"](https://embedded-systems-design.github.io/EGR314DataSheetTemplate/Appendix/01-Componet-Selection/Component-Selection-Process/#actuator) selection.

-----------
> Remove the following before submitting! Use them to present the selected components

## Module's Considered Major Components

### Secondary actuators

*Table 1: Secondary actuators component selection*
| **Component**                                                                                                                                                                                      | **Pros**                                                                                                           | **Cons**                                                                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ![](SERVO1.jpg)<br> SER0056 2KG 300 CLUTCH SERVO<br>$6/each<br>[link to product](https://www.digikey.com/en/products/detail/dfrobot/SER0056/13545236)  | \* Inexpensive<br>\* High torque<br>\*Clutch system and electrical protection prevents damage to motor when motor is blocked from rotating.<br> \* 300 degree range.<br> \* Easy to control with PWM signal.<br>\* Plastic gears make servo lighter, self lubricating, and more vibration dampening.<br>  | \* Cannot meet serial communication for actuator requirement.<br>\* 300 degree range is superfluous for design as only 180 degrees is required.<br>|
| ![](SERVO2.jpg)<br> SER0011 SERVOMOTOR RC 6V MICRO METAL GEAR<br>$8.62/each<br>[link to product](https://www.digikey.com/en/products/detail/dfrobot/SER0011/7087129) | \* Fairly inexpensive<br>\* 2.5 kg torque<br>\* Metal gears less likely to be stripped by softer structural links attached to motor.             | \*Cannot meeet serial communication for actuator requirement.


**Rationale:** A clock oscillator is easier ....

### Style 2

> Also acceptable, more markdown friendly

**External Clock Module**

1. XC1259TR-ND surface mount crystal

    ![](image1.png)

    * $1/each
    * [link to product](http://www.digikey.com/product-detail/en/ECS-40.3-S-5PX-TR/XC1259TR-ND/827366)

    | Pros                                      | Cons                                                             |
    | ----------------------------------------- | ---------------------------------------------------------------- |
    | Inexpensive                               | Requires external components and support circuitry for interface |
    | Compatible with PSoC                      | Needs special PCB layout.                                        |
    | Meets surface mount constraint of project |

**Rationale:** A clock oscillator is easier ...
