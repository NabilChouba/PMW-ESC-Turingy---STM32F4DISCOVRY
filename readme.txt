/**
init version of the program is from ST Discovery drivers
code modified to generate the PWM pulse needed for ESC-Truingy

Result and explanation is provided on the youtube video :
https://www.youtube.com/watch?v=1WU8XkjUNCQ
Instruction :
  - PMW signal 50Hz period 20ms
  - duty cycle period 1 ms during 4 second to disarm the ESC
  - max duty cycle is 2 ms ( full speed  )
  - min  duty cycle is 1 ms ( motor is off)

The ST Original example shows how to configure the TIM peripheral in PWM (Pulse Width Modulation)
mode.

The TIM3CLK frequency is set to SystemCoreClock / 2 (Hz), to get TIM3 counter
clock at 28 MHz the Prescaler is computed as following:
   - Prescaler = (TIM3CLK / TIM3 counter clock) - 1

SystemCoreClock is set to 168 MHz for STM32F4xx Devices Revision A.

The TIM3 is running at 42 KHz: TIM3 Frequency = TIM3 counter clock/(ARR + 1)
                                              = 28 MHz / 666 = 42 KHz
The TIM3 CCR1 register value is equal to 333, so the TIM3 Channel 1 generates a
PWM signal with a frequency equal to 30 KHz and a duty cycle equal to 50%:
TIM3 Channel1 duty cycle = (TIM3_CCR1/ TIM3_ARR + 1)* 100 = 50%

The TIM3 CCR2 register value is equal to 249, so the TIM3 Channel 2 generates a
PWM signal with a frequency equal to 30 KHz and a duty cycle equal to 37.5%:
TIM3 Channel2 duty cycle = (TIM3_CCR2/ TIM3_ARR + 1)* 100 = 37.5%

The TIM3 CCR3 register value is equal to 166, so the TIM3 Channel 3 generates a
PWM signal with a frequency equal to 30 KHz and a duty cycle equal to 25%:
TIM3 Channel3 duty cycle = (TIM3_CCR3/ TIM3_ARR + 1)* 100 = 25%

The TIM3 CCR4 register value is equal to 83, so the TIM3 Channel 4 generates a
PWM signal with a frequency equal to 30 KHz and a duty cycle equal to 12.5%:
TIM3 Channel4 duty cycle = (TIM3_CCR4/ TIM3_ARR + 1)* 100 = 12.5%

The PWM waveform can be displayed using an oscilloscope.


@par Directory contents

  - TIM_PWM_Output/stm32f4xx_conf.h     Library Configuration file
  - TIM_PWM_Output/stm32f4xx_it.c       Interrupt handlers
  - TIM_PWM_Output/stm32f4xx_it.h       Interrupt handlers header file
  - TIM_PWM_Output/main.c               Main program
  - TIM_PWM_Output/system_stm32f4xx.c   STM32F4xx system clock configuration file



@par Hardware and Software environment

  - This example runs on STM32F4xx Devices Revision A.

  - This example has been tested with STM32F4-Discovery (MB997) RevA and can be
    easily tailored to any other development board.

  - STM32F4-Discovery
    - Connect the following pins to an oscilloscope to monitor the different
      waveforms:
        - PC.06: (TIM3_CH1)
        - PC.07: (TIM3_CH2)
        - PB.00: (TIM3_CH3)
        - PB.01: (TIM3_CH4)

@par How to use it ?

In order to make the program work, you must do the following :

 + EWARM
    - Open the TIM_PWM_Output.eww workspace
    - Rebuild all files: Project->Rebuild all
    - Load project image: Project->Debug
    - Run program: Debug->Go(F5)
 */
