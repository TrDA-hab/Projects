# What it can be used for: 
the control of horizontal curtain or vertical shutters, blinds adjuster or window opener, pet feeders, opening of a water tap for watering the lawn, rotating table for subject photography, opening the ventilation flap, PTZ camera, 3D Scanner Table, linear Actuator.

# 1. MX1508 Motor Driver.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/901.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/902.jpg)

### How to use it:  
 - You must add support for Shutter in my_user_config.h file.
 - Run the commands in the console (you must first configure the GPIO!):  
    `ShutterMode 1`   // Enabling "Shutter mode 1"  
    `ShutterOpenDuration 2`   // Shutter opening time = 2 seconds  
    `ShutterCloseDuration 2`  // Shutter closing time = 2 seconds  
    `Restart 1`   // Restart Tasmota  

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D1|5|Relay2|CW
D2|4|Relay1|CCW

### Note:
 - you cannot control the RPM of the DC motor

### More information:
 - [About shutter](https://tasmota.github.io/docs/Blinds-and-Shutters/)
 - [Shutter commands](https://tasmota.github.io/docs/Commands/#shutters)

### Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20201224_144050.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/902-1.jpg)

# 2. TB6612FNG Motor Driver.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/903.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/904.jpg)

### How to use it:
 - You must add support for Shutter in my_user_config.h file.
 - Run the commands in the console (you must first configure the GPIO!):  
    `ShutterMode 1`   // Enabling "Shutter mode 1"  
    `ShutterOpenDuration 2`   // Shutter opening time = 2 seconds  
    `ShutterCloseDuration 2`  // Shutter closing time = 2 seconds  
    `Restart 1`   // Restart Tasmota  

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D6|12|Relay1|CW
D7|13|Relay2|CCW
D8|15|PWM1|PWM

### Note:
 - you can control the RPM of the DC motor !

### More information:
 - [About shutter](https://tasmota.github.io/docs/Blinds-and-Shutters/)
 - [Shutter commands](https://tasmota.github.io/docs/Commands/#shutters)

### Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210103_181349.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/904-1.jpg)

# 3. Wemos motor shield V1.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/905.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906.jpg)

Wemos Pin|GPIO|Component
:-:|:-:|:-:
D1|5|I2C SCL
D2|4|I2C SDA

If you did everything correctly, then in the console you should see this message:  
`00:00:00.062 I2C: WEMOS_MOTOR_V1 found at 0x30`

### Note:
Now (01/15/2021) Tasmota has no support for "Wemos motor shield V2". Perhaps this support will be added later.


`stm32flash.exe COM4`  
![1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-1.jpg)  
`stm32flash.exe -k COM4`  
![2](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-2.jpg)  
`stm32flash.exe -f -v -w motor_shield.bin COM4`  
![3](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-3.jpg)  

### Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210103_190344.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906-1.jpg)

Best regards
TrDA
