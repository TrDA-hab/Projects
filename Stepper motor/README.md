# 1. One stepper motor (minimum configuration):  
### Device List:  
 - 28BYJ-48-12V (stepper motor with 64:1 gear reducer).  
 - A4988 (stepper motor driver).  
 - ESP-01S (ESP8266 series wireless module).  
 - K7803-500R3 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4102.jpg)  

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file.
 - Or flash your ESP8266 module with `tasmota.bin` file.
 - Run commands in the console to run the "Stepper" mode (you must first configure the GPIO!):  
    `SetOption80 1`   // Set "Shutter" mode.   
    `ShutterMode 4`   // Enable "Shutter mode 4".  
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the console to configure the motor operation (you must first configure the GPIO!):  
    `ShutterFrequency 2500`   // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 2.5`  // Acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration 20`  // Shutter opening time = 20 seconds (default = 10 seconds).  
    `ShutterCloseDuration 20` // Shutter closing time = 20 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the consolee to configure the motor operation (you must first configure the GPIO!):      
    `ShutterOpen`   // Opening check.    
    `ShutterStop`   // Stop check.    
    `ShutterClose`  // Closing check.  

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

Wemos Pin|GPIO|Component|Stepper Signal
:-:|:-:|:-:|:-:
D1|5|Relay1i|EN
D2|4|Relay2|DIR
D3|0|PWM1|STP
D4|2|Counter1|STP
D6|5|SCL|INA219
D7|4|SLA|INA219
RX|3|Button1|Up button
TX|1|Button2|Down button


# 3. Two stepper motors (medium configuration):
### Device List:
 - Nema-17 (stepper motor).
 - DRV8825 (stepper motor driver).
 - Wemos D1 mini (ESP8266 series wireless board).
 - MP1584 (DC/DC step-down module).
 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4122.jpg)

Wemos Pin|GPIO|Component|Stepper Signal
:-:|:-:|:-:|:-:
D1|5|Relay1i|EN
D2|4|Relay2|DIR
D3|0|PWM1|STP
D4|2|Counter1|STP
D5|14|Relay3i|EN
D6|12|Relay4|DIR
D7|13|PWM2|STP
D8|15|Counter2|STP
