---
title: Application Programming Interface
---

## Overview
This page is for describing the Application Programming Interface for controlling the Sable arm system control board. The arm control board is designed to use a UART serial interface for 7 different message types.

**Message type 1 - Enable/Disable robot arm**

|                 | **Byte 1** | **Byte 2** |
| --------------- | ---------- | ---------- |
| Variable name | msg_type | EN       |
| Variable type | uint8_t  | uint8_t  |
| Min value     | 1        | 0        |
| Max value     | 7        | 1        |
| Example       | 1        | 1        |

**Message type 2 - State of robot arm**

|               |**Byte 1**|**Byte 2**|
|---------------|----------|----------|
| Variable name | msg_type | armIsOn  |
| Variable type | uint8_t  | uint8_t  |
| Min value     | 1        | 0        |
| Max value     | 7        | 1        |
| Example       | 2        | 1        |

**Message type 3 - Position offest from arm end effector position X, Y, Z**

|               |**Byte 1**|**Byte 2**|**Byte 3**|**Byte 4**|
|---------------|----------|----------|----------|----------|
| Variable name | msg_type | X_pos    | Y_pos    | Z_pos    |
| Variable type | uint8_t  | uint8_t  | uint8_t  | uint8_t  |
| Min value     | 1        | 0        | 0        | -10      |
| Max value     | 7        | 60       | 60       | 60       |
| Example       | 3        | 34       | 10       | 15       |

**Message type 4 - Arm success/failure to reach position**

|               |**Byte 1**|**Byte 2**|**Byte 3**|**Byte 4**|**Byte 5**|
|---------------|----------|----------|----------|----------|----------|
| Variable name | msg_type | X_pos    | Y_pos    | Z_pos    |state     |
| Variable type | uint8_t  | uint8_t  | uint8_t  | uint8_t  |uint8_t   |
| Min value     | 1        | 0        | 0        | -10      |0         |
| Max value     | 7        | 60       | 60       | 60       |1         |
| Example       | 4        | 34       | 10       | 15       |1         |

**Message type 5 - Arm collect/deposit sample**

|               |**Byte 1**|**Byte 2**|
|---------------|----------|----------|
| Variable name | msg_type | ser_claw |
| Variable type | uint8_t  | uint8_t  |
| Min value     | 1        | 0        |
| Max value     | 7        | 1        |
| Example       | 5        | 0        |

**Message type 6 - Arm collection/deposit completed**

|               |**Byte 1**|**Byte 2** |**Byte 3** |
|---------------|----------|-----------|-----------|
| Variable name | msg_type | collected | deposited |
| Variable type | uint8_t  | uint8_t   | uint8_t   |
| Min value     | 1        | 0         | 0         |
| Max value     | 7        | 1         | 1         |
| Example       | 6        | 0         | 1         |

**Message type 7 - Collection finished, Drive OK to move**

|               |**Byte 1**|**Byte 2**|
|---------------|----------|----------|
| Variable name | msg_type | DRV_OK   |
| Variable type | uint8_t  | uint8_t  |
| Min value     | 1        | 0        |
| Max value     | 7        | 1        |
| Example       | 7        | 0        |