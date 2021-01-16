# What it can be used for: 
the control of horizontal curtain or vertical shutters, blinds adjuster or window opener, pet feeders, opening of a water tap for watering the lawn, rotating table for subject photography, opening the ventilation flap, PTZ camera, 3D Scanner Table, linear Actuator.

# 1. MX1508 Motor Driver.

![901](https://user-images.githubusercontent.com/56403720/103483573-3ec18f00-4df9-11eb-92f5-2e507bf39e81.jpg)
![902](https://user-images.githubusercontent.com/56403720/103483578-43864300-4df9-11eb-9c7e-61d11d40a433.jpg)

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
![20201224_144050](https://user-images.githubusercontent.com/56403720/103483767-97455c00-4dfa-11eb-8e41-f09199c64090.jpg)
![902-1](https://user-images.githubusercontent.com/56403720/103483770-9ca2a680-4dfa-11eb-937e-5be729167769.jpg)

# 2. TB6612FNG Motor Driver.
![903](https://user-images.githubusercontent.com/56403720/103484034-b04f0c80-4dfc-11eb-8e85-094c5e4c98e7.jpg)
![904](https://user-images.githubusercontent.com/56403720/103487136-2f9c0a80-4e14-11eb-8649-ef003193efce.jpg)

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
![20210103_181349](https://user-images.githubusercontent.com/56403720/103484117-6ca8d280-4dfd-11eb-9fb2-0092a9cf9b79.jpg)
![904-1](https://user-images.githubusercontent.com/56403720/103484119-70d4f000-4dfd-11eb-90f1-f206ba64f56e.jpg)

# 3. Wemos motor shield V2.
![905](https://user-images.githubusercontent.com/56403720/103484157-ab3e8d00-4dfd-11eb-994c-e4c4068083b8.jpg)
![906](https://user-images.githubusercontent.com/56403720/103484161-b1cd0480-4dfd-11eb-8d08-c48d5672a7b7.jpg)

### Note:
I have not been able to test this driver at this time:
  - maybe this function is disabled in Tasmota.
  - or my driver is damaged (I will have a new one soon)
  - [Datasheet](https://www.wemos.cc/en/latest/d1_mini_shield/motor.html)

### Additional Information:
![20210103_190344](https://user-images.githubusercontent.com/56403720/103484187-d5904a80-4dfd-11eb-9f21-dd90526ad8c4.jpg)
![906-1](https://user-images.githubusercontent.com/56403720/103484196-dcb75880-4dfd-11eb-834e-9016ecf6dfb4.jpg)

Best regards
TrDA
