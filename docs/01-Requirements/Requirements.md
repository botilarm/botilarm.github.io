---
title: Arm Module's Requirements
---

## Arm Module Requirements
The following table documents the requirements for the arm system of the ground search and rescue drone.

| **Requirement Description** | **Measure of<br> Threshold** | **Target<br>Measure** |**Stretch<br>Requirement<br>(Y-N)**|
|-----------------------------| ----------------- | ----------------- | :-----: |
| Surface mounted, 3.3V switching power regulator | 3.2 Volts | 3.3 Volts | NO |
| Surface mounted microcontroller | uses 1 PIC or ESP | uses ESP32 | NO |
| Wireless Communication | Able to send or receive a Wi-Fi data | Send and receive Wi-Fi Data to MQTT | Yes |
| I2C or SPI | At least one actuator uses I2C or SPI to communicate with microcontroller | same as MoT | NO |
| Motors for arm must be permitted actuators | Motor creates outside motion, requires custom non-trivial interface circuit or filtered analog input to connect to micrcontroller | Creates outside motion and uses custom non-trivial interface circuit to connect to microcontroller. | NO |
| Software control of arm must not simply toggle a digital pin on and off. | Microcontroller does inverse kinematics to determine input to motors. | same as MoT | NO |
| Stable while moving | Arm can still hold objects while driving at least 5 mph over dirt and gravel. | Arm can still hold objects while driving at least 10 mph over dirt and gravel | NO |
| Human Design Interface; Respond manually with buttons | Can manually control all actuators on arm,  read sensor data, modify setpoints, and toggle GPIO debug pins.|Can do all that is required in MoT from exterior of device.| NO |
| Mechanism that can flip bot over if upside-down | Arm can flip over device when instrutions are ran to flip it over. | Flip over sequence succeeds 90% of the time and does not intefere with a 3x3 ft area around it.| YES |
| Mechanism to pick up, manipulate objects, and store objects | Can manipulate small solid objects (3x3x3 in. max, 1 lb) and move them to desired X, Y, Z, coordinates relative to drone. | Same as MoT | NO |
| Drone must be powered by onboard battery connected to a switching regulator. | Microcontroller and peripherals for arm are powered by a switching regulator connected to an onboard battery. | Same as MoT| NO |
