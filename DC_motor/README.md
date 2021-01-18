# What it can be used for: 
the control of horizontal curtain or vertical shutters, blinds adjuster or window opener, pet feeders, opening of a water tap for watering the lawn, rotating table for subject photography, opening the ventilation flap, PTZ camera, 3D Scanner Table, linear Actuator.

# 1. MX1508 Motor Driver.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/901.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/902.jpg)

### How to use it:  
 - You must add support for Shutter in my_user_config.h file.
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
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
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
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

### Note:
Now (01/15/2021) Tasmota has no support for "Wemos motor shield V2". Perhaps this support will be added later.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/905.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906.jpg)

### How to use it:

Wemos Pin|GPIO|Component
:-:|:-:|:-:
D1|5|I2C SCL
D2|4|I2C SDA

If you did everything correctly, then in the console you should see this message:  
`00:00:00.062 I2C: WEMOS_MOTOR_V1 found at 0x30`

1. You must add support for "WEMOS_MOTOR_V1" in my_user_config.h file.
2. Run commands in the console to test the motor (you must first configure the GPIO!):  
    `driver44 SETMOTOR, 0, 1`  // for CCW motor rotation  
    `driver44 SETMOTOR, 0, 3`  // for STOP motor  
    `driver44 SETMOTOR, 0, 2`  // for CW motor rotation 
    `driver44 SETMOTOR, 0, 4`  // for standby (optional)  
3. Use the rules to control the motor:   
    `Rule1`   
    `ON Power1#state=1 DO Backlog Power2 0; Power3 0; driver44 SETMOTOR, 0, 3; delay 10; driver44 SETMOTOR, 0, 1; delay 40; driver44 SETMOTOR, 0, 3; Power1 0 ENDON`   
    `ON Power2#state=1 DO Backlog Power1 0; Power3 0; driver44 SETMOTOR, 0, 3; Power2 0 ENDON`   
    `ON Power3#state=1 DO Backlog Power1 0; Power2 0; driver44 SETMOTOR, 0, 3; delay 10; driver44 SETMOTOR, 0, 2; delay 40; driver44 SETMOTOR, 0, 3; Power3 0 ENDON`   
  - `Rule1 1` // run rule1  
4. Add "logic" to the control buttons:
    `Backlog WebButton1 &#8648; WebButton2 Stop1; WebButton3 &#8650`


[More information!](https://github.com/arendst/Tasmota/blob/development/tasmota/xdrv_34_wemos_motor_v1.ino)  

### Note:
"WEMOS MOTOR V1" requires a firmware update. Factory installed firmware has reliability issues like I2C bus stuck. The firmware requires regular USB2TTL.
[More information!](https://hackaday.io/project/18439-motor-shield-reprogramming)  

WEMOS MOTOR Pin|GPIO|Component|USB2TTL
:-:|:-:|:-:|:-:
D1|5|RX|RX
D2|4|RX|RX
3V3|-|-|3V3
GND|-|-|GND

**! And be sure to short-circuit the RTS and 3V pins together on "Wemos motor shield V1".**

1. Download here for firmware "motor_shield.bin":
 - https://cdn.hackaday.io/files/18439788894176/motor_shield.bin

2. Download "STM32Flash" from here:
 - https://sourceforge.net/projects/stm32flash/files/

3. Run these commands in the Windows console (use your COM port number!):  
`stm32flash.exe COM4`  
`stm32flash.exe -k COM4`  
`stm32flash.exe -f -v -w motor_shield.bin COM4`  

![1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-1.jpg)  
![2](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-2.jpg)  
![3](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-3.jpg)  
  
**After finishing the firmware, disconnect all wires (including the 3V and RTS pin), connect the shield to the ESP device and it should work!**

### Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210103_190344.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906-1.jpg)

Best regards   
TrDA
