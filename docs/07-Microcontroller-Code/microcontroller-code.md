---
title: Microcontroller Code
---
## Overview
This code was used to verify subsystem functionality by converting an analog signal from an amplifier to a DC voltage, and displaying it, as well as sending a digital signal to verify that current is being sensed to the solenoid door latch board. It features code for switching the display from energy usage to instantaneous power but does not yet feature code to convert from the analog to digital signal to show either of those two values.

## main.c
```
#include "mcc_generated_files/system/system.h"
#include <stdio.h>
#include <stdbool.h>

/*
    Main application
*/

int main(void)
{
    SYSTEM_Initialize();
    ADC_Initialize();
    bool isEnergyMode = false;
    int analog_in;
    
    while(1)
    {
        //switch from instantanous power display to energy usage over time
        if(IO_PB_GetValue() == 1)
        {
            isEnergyMode = !isEnergyMode;
            LED1_SetHigh();
            //LED2_SetHigh();
            LED3_SetHigh();
            LED4_SetHigh();
            //waits until button is released
            while(IO_PB_GetValue() == 1);
        } else {
            LED1_SetLow();
            //LED2_SetLow();
            LED3_SetLow();
            LED4_SetLow();
        }
        
        //read analog current sensor value and check if current is being drawn
        ADC_ChannelSelect(ADC_CHANNEL_ANA0);
        ADC_ConversionStart();
        while (!ADC_IsConversionDone());
        analog_in = ADC_ConversionResultGet();
        printf("%d \r\n",analog_in);
        
        //send cur_debug signal to verify that device is plugged in
        if(analog_in > 700) CUR_D_SetHigh();
        else CUR_D_SetLow();
    }    
}
```

## Project Download
The code as an mplabx project download is available [*here*](sg_power_monitor.zip).