# What it can be used for: 
the control of horizontal curtain or vertical shutters, blinds adjuster or window opener, pet feeders, opening of a water tap for watering the lawn, rotating table for subject photography, opening the ventilation flap, PTZ camera, 3D Scanner Table, linear Actuator.

# 1. MX1508 Motor Driver.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/901.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/902.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/902-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210120_190559.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210120_212409.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210120_214905.jpg)

### Video of the driver's work:
 - https://youtu.be/9aGlk5LSMys

### Note:
 - you cannot control the RPM of the DC motor

### How to use it:  
 - You must add support for Shutter in my_user_config.h file.
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
    `ShutterMode 1`   // Enabling "Shutter mode 1"  
    `ShutterOpenDuration 2`   // Shutter opening time = 2 seconds  
    `ShutterCloseDuration 2`  // Shutter closing time = 2 seconds  
    `Restart 1`   // Restart Tasmota  
    `ShutterOpen`   // CW motor rotation  
    `ShutterClose`  // CWW motor rotation 

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D1|5|Relay2|CW
D2|4|Relay1|CCW

### More information:
 - [About shutter](https://tasmota.github.io/docs/Blinds-and-Shutters/)
 - [Shutter commands](https://tasmota.github.io/docs/Commands/#shutters)

# 2. TB6612FNG Motor Driver.
### More information:
 - [About shutter](https://tasmota.github.io/docs/Blinds-and-Shutters/)
 - [Shutter commands](https://tasmota.github.io/docs/Commands/#shutters)
 - [About TB6612FNG](https://www.pololu.com/product/713)

### Video of the driver's work:
 - https://youtu.be/e9kBO-Brymo
 - https://youtu.be/3fbM7FQ-1wY

## 2.1 Using ONE motor
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/903.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/904.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210103_181349.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210123_160002.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210123_155956.jpg)

### Note:
 - you can control the RPM of the DC motor !

### How to use it:
 - You must add support for Shutter in my_user_config.h file.
 - Run commands in the console (you must first configure the GPIO!):  
    `Rule1 ON system#boot DO Backlog Power3 1; Dimmer 75 ENDON `   // Enabling the driver and setting the PWM to 75%.  
    `Rule1 1`   // Enabling Rule1  
    `WebButton4 STBY`   // To rename a web button (optional)  
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
    `ShutterMode 1`   // Enabling "Shutter mode 1"  
    `Restart 1`   // Restart Tasmota  
    `ShutterOpen`   // test CW motor rotation  
    `ShutterClose`  // test CWW motor rotation 

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D5|14|Relay3|STBY
D6|12|Relay1|CW
D7|13|Relay2|CCW
D8|15|PWM1|PWM

## 2.2 Using DUAL motor.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/909.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/9010.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/909-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210315_224338.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210317_202159.jpg)

### Note:
 - you can control the RPM of the DC motors !

### How to use it:
 - You must add support for Shutter in my_user_config.h file.
 - Run commands in the console (you must first configure the GPIO!):  
    `SetOption68 1`   // Enable multi-channel PWM  
    `SetOption73 1`   // Enable detach buttons from relays  
    `Rule1 ON system#boot DO Backlog Power5 1; Power6 1; Power7 1; Channel6 50; Channel7 75 ENDON`   // Enable PWM to 50% and 75%.  
    `Rule1 1`   // Enable Rule1  
    `Backlog WebButton5 PWM1; WebButton6 PWM2; WebButton7 STNB`   // To rename a web button (optional)  
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
    `ShutterMode 1`   // Enabling "Shutter mode 1"  
    `ShutterRelay1 1`   // for relay Relay1 and Relay2  
    `ShutterRelay2 3`   // for relay Relay3 and Relay4  
    `Restart 1`   // Restart Tasmota  
    `ShutterOpen1`   // test CW motor1 rotation  
    `ShutterClose1`  // test CWW motor1 rotation 
    `ShutterOpen2`   // test CW motor2 rotation  
    `ShutterClose2`  // test CWW motor2 rotation  
    `ShutterButton1 1 updown 0`  // Assigns button#1 to act as an "up and down" button (1x press up, 2x press down) for Shutter#1   
    `ShutterButton2 2 updown 0`  // Assigns button#2 to act as an "up and down" button (1x press up, 2x press down) for Shutter#2    

ESP-01M Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D2|04|PWM1|PWM1 motor1
D6|12|Relay1|CW motor1
D7|13|Relay2|CCW motor1
FL|09|Button1|Up/Down#1
D4|02|PWM1|PWM2 motor2
D7|13|Relay3|CW# motor2
D8|15|Relay4|CCW motor2
FL|10|Button2|Up/Down#2
D5|14|Relay5|Stnb

# 3. Wemos motor shield.

### Video of the driver's work:
 - https://youtu.be/gah3zCJPPUc  
 - https://youtu.be/8P2wTgeavdo  

### More information:  
- https://www.wemos.cc/en/latest/d1_mini_shield/motor.html

## 3.1 Using ONE motor.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/905.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906.jpg)

### How to use it:

1. You must add support for "WEMOS_MOTOR_V1" in my_user_config.h file.
2. Сonfigure the GPIO:  

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D1|5|I2C SCL| ---
D2|4|I2C SDA| ---
D3|0|Relay1| CW motor1
D4|2|Relay2| Stop motor1
D5|14|Relay3| CCW motor1

  **If you did everything correctly, then in the console you should see this message:**  
   `00:00:00.062 I2C: WEMOS_MOTOR_V1 found at 0x30`

3. Run commands in the console to test the motor (you must first configure the GPIO!):  
    `driver44 SETMOTOR,0,1,80`  // for CCW motor1 (80% duty - optional)  
    `driver44 SETMOTOR,0,3`  // for STOP motor1  
    `driver44 SETMOTOR,0,2,80`  // for CW motor1 (80% duty - optional)  
    `driver44 SETMOTOR,0,4`  // for standby motor1 (optional)  
    [More information!](https://github.com/arendst/Tasmota/blob/development/tasmota/xdrv_34_wemos_motor_v1.ino)  
4. Use the rules to control the motor (optional):   
  - `Rule1`  // remove comments before using the rule!   
    `ON Power1#state=1 DO Backlog Power2 0; Power3 0; driver44 SETMOTOR,0,3; delay 10; driver44 SETMOTOR,0,1,80; delay 55; driver44 SETMOTOR,0,3; Power1 0 ENDON` // CW motor1, "delay 55" controls the opening (time 55 = 5.5 sec).   
    `ON Power2#state=1 DO Backlog Power1 0; Power3 0; driver44 SETMOTOR,0,3; Power2 0 ENDON` // Stop motor1   
    `ON Power3#state=1 DO Backlog Power1 0; Power2 0; driver44 SETMOTOR,0,3; delay 10; driver44 SETMOTOR,0,2,80; delay 55; driver44 SETMOTOR,0,3; Power3 0 ENDON` //CCW motor1, "delay 55" controls the closing  (time 55 = 5.5 sec).   
  - `Rule1 1`  //  run rule1   
5. Add "logic" to the control WEB buttons (optional):   
    `Backlog WebButton1 &#8648; WebButton2 Stop1; WebButton3 &#8650`   

## 3.2 Using DUAL motor.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/907.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/908.jpg)

### How to use it:

1. You must add support for "WEMOS_MOTOR_V2" in my_user_config.h file.
2. Сonfigure the GPIO:  

Wemos Pin|GPIO|Component|Motor Signal
:-:|:-:|:-:|:-:
D1|5|I2C SCL| ---
D2|4|I2C SDA| ---
D3|0|Relay1| CW motor1
D4|2|Relay2| Stop motor1
D5|14|Relay3| CCW motor1
D6|12|Relay4| CW motor2
D7|13|Relay5| Stop motor2
D8|15|Relay6| CCW motor2

  **If you did everything correctly, then in the console you should see this message:**  
   `00:00:00.062 I2C: WEMOS_MOTOR_V1 found at 0x30`

3. Run commands in the console to test the **motor1** (you must first configure the GPIO!):  
    `driver44 SETMOTOR,0,1,75`  // for CCW motor1 (75% duty - optional) 
    `driver44 SETMOTOR,0,3`  // for STOP motor1  
    `driver44 SETMOTOR,0,2,75`  // for CW motor1  (75% duty - optional)
    `driver44 SETMOTOR,0,4`  // for standby motor1 (optional)  
    [More information!](https://github.com/arendst/Tasmota/blob/development/tasmota/xdrv_34_wemos_motor_v1.ino)  
4. Run commands in the console to test the **motor2** (you must first configure the GPIO!):  
    `driver44 SETMOTOR,1,1,50`  // for CCW motor2 (50% duty - optional)  
    `driver44 SETMOTOR,1,3`  // for STOP motor2  
    `driver44 SETMOTOR,1,2,50`  // for CW motor2 (50% duty - optional)  
    `driver44 SETMOTOR,1,4`  // for standby motor2 (optional)  
    [More information!](https://github.com/arendst/Tasmota/blob/development/tasmota/xdrv_34_wemos_motor_v1.ino) 
6. Use the rules to control the **motor1** and **motor2** (optional):   
  - `Rule1`  // remove comments before using the rule!   
    `ON Power1#state=1 DO Backlog Power2 0; Power3 0; driver44 SETMOTOR,0,3; delay 10; driver44 SETMOTOR,0,1,75; delay 69; driver44 SETMOTOR,0,3; Power1 0 ENDON` //  CW motor1, "delay 69" controls the opening (time 69 = 6.9 sec.)"   
    `ON Power2#state=1 DO Backlog Power1 0; Power3 0; driver44 SETMOTOR,0,3; Power2 0 ENDON` //  Stop motor1   
    `ON Power3#state=1 DO Backlog Power1 0; Power2 0; driver44 SETMOTOR,0,3; delay 10; driver44 SETMOTOR,0,2,75; delay 69; driver44 SETMOTOR,0,3; Power3 0 ENDON` //  CCW motor1, "delay 69" controls the closing  (time 69 = 6.9 sec).   
  - `Rule1 1` // run rule1  
  
  - `Rule2`  // remove comments before using the rule!   
    `ON Power4#state=1 DO Backlog Power5 0; Power6 0; driver44 SETMOTOR,1,3; delay 10; driver44 SETMOTOR,1,1,50; delay 77; driver44 SETMOTOR,1,3; Power4 0 ENDON` //  CW motor2, "delay 77" controls the opening (time 77 = 7.7 sec).   
    `ON Power5#state=1 DO Backlog Power4 0; Power6 0; driver44 SETMOTOR,1,3; Power5 0 ENDON` //  Stop motor2    
    `ON Power6#state=1 DO Backlog Power4 0; Power5 0; driver44 SETMOTOR,1,3; delay 10; driver44 SETMOTOR,1,2,50; delay 77; driver44 SETMOTOR,1,3; Power6 0 ENDON` //  CCW motor2, "delay 77" controls the closing  (time 77 = 7.7 sec).    
  - `Rule2 1` // run rule2  
6. Add "logic" to the control WEB buttons (optional):   
    `Backlog WebButton1 &#8648; WebButton2 Stop1; WebButton3 &#8650`  
    `Backlog WebButton4 &#8634; WebButton5 Stop2; WebButton6 &#8635`  

### Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210103_190344.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/906-1.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210120_190830.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210124_174710.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/20210124_174415.jpg)

# Note!!! :
"WEMOS MOTOR V1" requires a firmware update. Factory installed firmware has reliability issues like I2C bus stuck. The firmware requires regular USB2TTL.
[More information!](https://hackaday.io/project/18439-motor-shield-reprogramming)  

WEMOS MOTOR Pin|GPIO|Component|USB2TTL
:-:|:-:|:-:|:-:
D1|5|RX|TX
D2|4|TX|RX
3V3|-|-|3V3
GND|-|-|GND

**!!! And be sure to short-circuit the RTS and 3V pins together on "Wemos motor shield V1".**

1. Download here for firmware "motor_shield.bin":
 - https://cdn.hackaday.io/files/18439788894176/motor_shield.bin   
 or   
 - https://github.com/TrDA-hab/Projects/blob/master/DC_motor/motor_shield.bin   

2. Download "STM32Flash" from here:
 - https://sourceforge.net/projects/stm32flash/files/

3. Run these commands in the Windows console (use your COM port number!):  
`stm32flash.exe COM4`  
`stm32flash.exe -k COM4`  
`stm32flash.exe -f -v -w motor_shield.bin COM4`  

![1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-1.jpg)  
![2](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-2.jpg)  
![3](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/STM32flash-3.jpg)  
  
**!!! After finishing the firmware, disconnect all wires (including the 3V and RTS pin), connect the shield to the ESP device and it should work!**

## 3.3 Using Wemos motor shield HR8833 Motor Shield (now no tested).   
![1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/hr8833_v1.0.0_1_16x16.jpg)   
https://www.wemos.cc/en/latest/d1_mini_shield/hr8833_motor.html   
https://aliexpress.com/item/1005003697301523.html   

## 3.4 Using Wemos motor shield AT8870 Motor Shield (now no tested).    
![1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor/at8870_v1.0.0_1_16x16.jpg)   
https://www.wemos.cc/en/latest/d1_mini_shield/at8870_motor.html   
https://aliexpress.com/item/1005003800396010.html   

**Best regards,   
TrDA.**
