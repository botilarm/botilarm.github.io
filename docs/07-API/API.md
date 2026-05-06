---
title: Application Programming Interface
---

## Overview
This page is for describing the Application Programming Interface for controlling the Sable arm system control board. The arm control board is designed to use a UART serial interface for 2 different message types, with a third message for debugging, displayed to the HMI interface which indicates that the arm is in dir, speed, and revs mode.

**Message type 1 - Enable/Disable robot arm**

|                 | **Byte 1** |
| --------------- | ---------- |
| Variable name   | armIsOn    |
| Variable type   | bytearray  |
| Min value       | 0          |
| Max value       | 1          |
| Example         | 1          |

**Message type 2 - Direction, Speed, and Revolutions**

|               |**Byte 1**|**Byte 2**|**Byte 3**|
|---------------|----------|----------|----------|
| Variable name |    DIR   | SPEED    | REVS     |
| Variable type | uint8_t  | uint8_t  | uint8_t  |
| Min value     | 0        | 0        | 0        |
| Max value     | 1        | 9        | 9        |
| Example       | 1        | 6        | 9        |

## Microcontroller Code
Shown below is the [main.py](main.py) microypthon code for the esp32. It uses the TMC2209_ESP32 library found here: [https://github.com/kjk25/TMC2209_ESP32](https://github.com/kjk25/TMC2209_ESP32), with the only modification being that all the python files are in the same directory as main.py.

```
from TMC_2209_StepperDriver import *
import ssl
import uasyncio as asyncio
from machine import UART
from machine import Pin
from time import sleep

## PINS
#-----------------------------------------------------------------------
ledPWR = Pin(8, Pin.OUT)
ledPWR.value(1) #Power on LED
ledRDY = Pin(17, Pin.OUT)
ledMOV = Pin(18, Pin.OUT)
ledDBG1 = Pin(16, Pin.OUT)
ledDBG2 = Pin(15, Pin.OUT)

# TMC2209
#----------------
tmc = TMC_2209(35, 36, 37)

# Debug pins setup
debugPB = Pin(4, Pin.OUT)

# USER / TEAM CONFIG
MY_ID = b'A'  # Your ID
TEAM = [b'M', b'C', b'A', b'L', b'V', b'K']  # valid team members
MAX_MSG_LEN = 32

should_stop = False

# MESSAGE PARSER
#-----------------------------------------------------------------------
def parse_message(msg):
    try:
        if not msg.startswith(b'AZ') or not msg.endswith(b'YB'):
            return None, "FORMAT_ERROR"

        core = msg[2:-2]  # remove AZ and BY

        if len(core) < 2:
            return None, "FORMAT_ERROR"

        src = core[0:1]
        dest = core[1:2]
        body = core[2:]

        if len(body) > MAX_MSG_LEN:
            return None, "TOO_LONG"

        if src not in TEAM:
            return None, "UNKNOWN_SENDER"

        

        return (src, dest, body), None

    except Exception:
        return None, "PARSE_FAIL"
    

        
    
# UART 1 SETUP
#----------------------------------------------------------------------
# initiate UART 1 for interboard communication
#----------------------------------------------------------------------
uart = UART(1, 9600,tx=38,rx=48)
uart.init(9600, bits=8, parity=None, stop=1, flow=0)

## COMMAND TASK
#----------------------------------------------------------------------
async def runCommand(command):
    #start/stop motor
    if command == b'1':
        tmc.setMotorEnabled(1)
        should_stop = False
    elif command == b'0':
        tmc.setMotorEnabled(0)
        should_stop = True
        # direction, speed, and revolution count control
    elif len(command) == 3: #first check if length of command is correct; it should be 3 bytes for dir and speed, and revolution
        
        print("DIR, SPEED, AND REVS MODE SELECTED")
        print("DIR = ", command[0] - 48, ", SPEED = ", (command[1] - 48)*100, ", REVS = ", command[2] - 48)
        #snd info over over uart
        uart.write(b'AZALDIR SPEED AND REVS SELECTEDYB')
        async.
        if command[0] - 48 == 0:
            tmc.setDirection_reg(False)
        else:
            tmc.setDirection_reg(True)
        #tmc.setDirection_pin(command[0] - 48)
        tmc.setMaxSpeed((command[1] - 48)*100)
        tmc.setAcceleration(2000)
        tmc.runToPositionRevolutions(command[2] - 48)
    else:
        print("ERROR: MOTOR DISABLED, MOTOR MUST RECEIVE START COMMAND TO BE ENABLED")

#----------------------------------------------------------------------
# UART RECEIVER TASK
#----------------------------------------------------------------------
async def receiver():
    b = b''
    sreader = asyncio.StreamReader(uart)
    print("UART1 TX LIVE")
    while True:
        #detect message and add to buffer
        res = await sreader.read(1)
        if not res:
            continue
        b += res
        
        #detect end of message
        if b.endswith(b'YB'):
           print("UART1 RX:", b)
           parsed, error = parse_message(b)
           if error:
               print("UART ERROR", error)
               b = b''
               continue
           src, dest, body = parsed
           
           if dest == MY_ID:
               print("UART message for ME")
               print("FROM:", src.decode(), "Message:", body.decode())
               asyncio.create_task(runCommand(body))
           else:
               print("UART message for ", dest.decode())
               print("Forwarding via UART")
               uart.write(b)
           b = b''
## TMC
#-----------------------------------------------------------------------
# initiate the TMC_2209 class
# use your pins for pin_step, pin_dir, pin_en here
#-----------------------------------------------------------------------
tmc = TMC_2209(35, 36, 37)

#-----------------------------------------------------------------------
# set the loglevel of the libary (currently only printed)
# set whether the movement should be relative or absolute
# both optional
#-----------------------------------------------------------------------
tmc.setLoglevel(Loglevel.debug)
tmc.setMovementAbsRel(MovementAbsRel.relative)

#-----------------------------------------------------------------------
# these functions change settings in the TMC register
#-----------------------------------------------------------------------
tmc.setDirection_reg(False)
tmc.setVSense(True)
tmc.setCurrent(300)
tmc.setIScaleAnalog(True)
tmc.setInterpolation(True)
tmc.setSpreadCycle(False)
tmc.setMicrosteppingResolution(1)
tmc.setInternalRSense(False)

print("---\n---")

# MAIN CODE
#----------------------------------------------------------------------
# Device waits for UART communication
# If UART message is for device, either number of steps or direction and speed, device destroys message and carrys out action
#----------------------------------------------------------------------


        
async def main():
    #Stays here indefinitely becasue receiver is an infinite loop
    await receiver()
    
try:
    #run main code
    asyncio.run(main())
finally:
    #if program finishes, cancel current loop and pre-load new one
    loop = asyncio.get_event_loop()
    loop.close
    asyncio.new_event_loop()
```