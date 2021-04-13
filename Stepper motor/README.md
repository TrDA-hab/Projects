# 1. One stepper motor (minimum configuration):  
### Device List:  
 - 28BYJ-48-12V (stepper motor with 64:1 gear reducer).  
 - A4988 (stepper motor driver).  
 - ESP-01S (ESP8266 series wireless module).  
 - K7803-500R3 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4102.jpg)  

### How to use it:  
 - You must add support for Shutter in my_user_config.h file.
 - Run commands in the console to test the motor (you must first configure the GPIO!):  
    `SetOption80 1`   // Enable "Shutter"   
    `ShutterMode 4`   // Enable "Shutter mode 4"  
    `ShutterOpenDuration 2`   // Shutter opening time = 2 seconds  
    `ShutterCloseDuration 2`  // Shutter closing time = 2 seconds  
    `Restart 1`   // Restart Tasmota  
    `ShutterOpen`   // CW motor rotation  
    `ShutterClose`  // CWW motor rotation 

Wemos Pin|GPIO|Component|Stepper Signal
:-:|:-:|:-:|:-:
D1|5|Relay1i|EN
D2|4|Relay2|DIR
D3|0|PWM1|STP
D4|2|Counter1|STP

# 2. One stepper motor (maximum configuration):
### Device List:
 - Nema-17 (stepper motor).
 - DRV8825 (stepper motor driver).
 - Wemos D1 mini (ESP8266 series wireless board).
 - INA219 (power-monitoring board).
 - MP1584 (DC/DC step-down moduler).

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4112.jpg)

# 3. Two stepper motors (medium configuration):
### Device List:
 - Nema-17 (stepper motor).
 - DRV8825 (stepper motor driver).
 - Wemos D1 mini (ESP8266 series wireless board).
 - MP1584 (DC/DC step-down module).
 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4122.jpg)
