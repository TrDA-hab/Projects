## 0. About using stepper motors.
- Using "Shutters mode" you can also simply control the:
  - DC motors using this [instruction.](https://github.com/arendst/Tasmota/discussions/10387) 
  - Servo motors using this [instruction](https://github.com/arendst/Tasmota/discussions/10443)
  - Stepper motors using this instruction (see instructions below).    
- You can only use [**bipolar**](https://en.wikipedia.org/wiki/Stepper_motor) stepper motor using this instruction, [**unipolar**](https://en.wikipedia.org/wiki/Stepper_motor) stepper motor not supported. 
- To work with stepper motors you need to use **Shutters mode**:
  - [More information about Shutters mode.](https://tasmota.github.io/docs/Blinds-and-Shutters)   
  - [More information on commands for Shutters mode.](https://tasmota.github.io/docs/Commands/#shutters)   
- Now it is highly recommended to use stepper motor driver TMC2208 instead of А4988/DRV8825.   
- And it is highly recommend using the power supply of 24 volts for your projects, minimum recommended voltage 12 volts.
- Modifying a 28BYJ-48-12V stepper motor from unipolar to bipolar [tutorial](https://coeleveld.com/wp-content/uploads/2016/10/Modifying-a-28BYJ-48-step-motor-from-unipolar-to-bipolar.pdf).     
- More information about [28BYJ-48](https://lastminuteengineers.com/28byj48-stepper-motor-arduino-tutorial/). 
- The diagrams show the supply voltage of the NEMA-17 stepper motor, capacitor should be 35 ... 50 volts. More information about the effect of voltage on stepper motor operation can be found in the [tutorial:](http://stepcontrol.com/pdf/step101.pdf) (see 5. POWER SUPPLY):  
   - for 28BYJ-48-**5v** recommended voltage is 12v (only if modifying to bipolar).
   - for 28BYJ-48-**12v** recommended voltage is 24v (only if modifying to bipolar).
- Stepper drivers configuration tutorials:
   - [A4988](https://lastminuteengineers.com/a4988-stepper-motor-driver-arduino-tutorial/)  
   - [DRV8825](https://lastminuteengineers.com/drv8825-stepper-motor-driver-arduino-tutorial/)  
   - [TMC2208](https://wiki.fysetc.com/TMC2208/)  
 - Don't forget to customize the microstep (MS1/MS2/MS3) for your needs (see tutorials above).
 - Remember to set the current limiting for your stepper motor driver (see tutorials above).
 - To reverse the rotation of the stepper motor, you must swap the two coils in the mirror image.  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/c5.jpg)  

Original motor Wiring|Reverse motor Wiring
:-:|:-:|
![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=RED&color=red)|
![](https://img.shields.io/static/v1?label=&message=GEEN&color=greem)|![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|
![](https://img.shields.io/static/v1?label=&message=RED&color=red)|![](https://img.shields.io/static/v1?label=&message=GEEN&color=greem)|
![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|

# 1. One stepper motor (minimum configuration):  
### Device List:  
 - 28BYJ-48-12V (stepper motor with 64:1 gear reducer).  
 - A4988 (stepper motor driver).  
 - ESP-01S (ESP8266 series wireless module).  
 - K7803-500R3 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4102.jpg)  

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file (оr flash your ESP8266 module with `tasmota.bin` file).  
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`   // Enable shutters support.   
    `ShutterMode 4`   // Enable "Shutter mode 4".  
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the console to configure the motor operation (you must first configure the GPIO!):  
    `ShutterFrequency 2500`   // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 2.5`  // Acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration1 20`  // Shutter opening time = 20 seconds (default = 10 seconds).  
    `ShutterCloseDuration1 20` // Shutter closing time = 20 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the consolee to test the motor operation (you must first configure the GPIO!):      
    `ShutterOpen1`   // Opening check.    
    `ShutterStop1`   // Stop check.    
    `ShutterClose1`  // Closing check.  
  -  Perform the [shutter calibration](Blinds-and-Shutters.md#calibration) (Optional).  

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

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file.  
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`   // Enable shutters support.   
    `ShutterMode 4`   // Enable "Shutter mode 4".  
    `ShutterRelay2 3`   // For relay Relay3i and Relay4.      
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the console to configure the motor operation (you must first configure the GPIO!):  
    `ShutterFrequency 2500`   // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 2.5`  // Acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration1 20`  // Shutter opening time = 20 seconds (default = 10 seconds).  
    `ShutterCloseDuration1 20` // Shutter closing time = 20 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota  
  -  Run commands in the consolee to test the motor operation (you must first configure the GPIO!):      
    `ShutterOpen1`   // Opening check.    
    `ShutterStop1`   // Stop check.    
    `ShutterClose1`  // Closing check.  
  -  Perform the [shutter calibration](Blinds-and-Shutters.md#calibration) (Optional).

Wemos Pin|GPIO|Component|Stepper Signal
:-:|:-:|:-:|:-:
D1|5|Relay1i|EN
D2|4|Relay2|DIR
D3|0|PWM1|STP
D4|2|Counter1|STP
D6|12|SCL|INA219
D7|13|SLA|INA219
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
