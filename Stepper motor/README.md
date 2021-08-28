## 0. Credits.
- @stefanbode (Stefan Bode / DE), developed and strongly promoted "Shutter mode".Efficiency 73.99% - the work was done by this very cool man.  
- @meingraham (Michael Ingraham / USA), Efficiency 25.00% - brilliantly organized the work to create support for "Shutter mode" at the end of 2019.  
- @TrDA-hab (Dmitriy Tretnyakov / RUS), Efficiency 00.01% - this is me, you can see my work below.  

## 1. About using stepper motors.
- Using "Shutters mode" you can also simply control the:
  - DC motors using this [instruction.](https://github.com/arendst/Tasmota/discussions/10387) 
  - Servo motors using this [instruction.](https://github.com/arendst/Tasmota/discussions/10443)
  - You can see a practical example of using a stepper motor here [here.](https://github.com/arendst/Tasmota/discussions/10847)
  - Stepper motors using this instruction (see instructions below).    
- You can only use [**bipolar**](https://en.wikipedia.org/wiki/Stepper_motor) stepper motor using this instruction, [**unipolar**](https://en.wikipedia.org/wiki/Stepper_motor) stepper motor not supported. 
- Types of Steppers [(**1**)](https://learn.adafruit.com/all-about-stepper-motors/types-of-steppers).
- To work with stepper motors you need to use **Shutters mode**:
  - [More information about Shutters mode.](https://tasmota.github.io/docs/Blinds-and-Shutters)   
  - [More information on commands for Shutters mode.](https://tasmota.github.io/docs/Commands/#shutters)   
- Now it is highly recommended to use stepper motor driver **TMC2208** instead of А4988/DRV8825.   
- And it is highly recommend using the power supply of **24 volts** for your projects, minimum recommended voltage 12 volts.
- Modifying a 28BYJ-48 stepper motor from unipolar to bipolar [tutorial](https://coeleveld.com/wp-content/uploads/2016/10/Modifying-a-28BYJ-48-step-motor-from-unipolar-to-bipolar.pdf).     
- More information about [28BYJ-48](https://lastminuteengineers.com/28byj48-stepper-motor-arduino-tutorial/). 
- The diagrams show the supply voltage of the NEMA-17 stepper motor, capacitor should be 35 ... 50 volts. More information about the effect of voltage on stepper motor operation can be found in the [tutorial:](http://stepcontrol.com/pdf/step101.pdf) (see 5. POWER SUPPLY):  
   - for 28BYJ-48-**5v** recommended voltage is 12v (only if modifying to bipolar).
   - for 28BYJ-48-**12v** recommended voltage is 24v (only if modifying to bipolar).
- Stepper drivers configuration tutorials:
   - [A4988](https://lastminuteengineers.com/a4988-stepper-motor-driver-arduino-tutorial/)  
   - [DRV8825](https://lastminuteengineers.com/drv8825-stepper-motor-driver-arduino-tutorial/)  
   - [TMC2208](https://wiki.fysetc.com/TMC2208/)  
 - Don't forget to customize the microstep (MS1/MS2/MS3) for your needs (see tutorials above). If you forget or incorrectly adjust the microstepping mode you will get the same effect as in this [video](https://youtu.be/1llRwfUVu5Q). Each stepper motor driver must use its own microstepping mode.   
 - Remember to set the current limiting for your stepper motor driver (see tutorials above).
 - To reverse the rotation of the stepper motor, you must swap the two coils in the mirror image. Software reverse rotation of the motor is not supported.    
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/c5.jpg)  

Original motor Wiring|Reverse motor Wiring
:-:|:-:|
![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=RED&color=red)|
![](https://img.shields.io/static/v1?label=&message=GEEN&color=greem)|![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|
![](https://img.shields.io/static/v1?label=&message=RED&color=red)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|
![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|![](https://img.shields.io/static/v1?label=&message=GEEN&color=greem)|

# 2. One stepper motor (minimum configuration):  
### Device List:  
 - 28BYJ-48-12V (stepper motor with 64:1 gear reducer).  
 - A4988 (stepper motor driver).  
 - ESP-01S (ESP8266 series wireless module).  
 - K7803-500R3 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4101.jpg) 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4102.jpg)  

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file (оr flash your ESP8266 module with `tasmota.bin` file).  
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`   // Enable shutters support.   
    `ShutterMode 4`   // Enable "Shutter mode 4".  
    `Restart 1`   // Restart Tasmota.  
  -  Run commands in the console to configure the motor operation:  
    `ShutterFrequency 2500`   // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 2.5`  // Acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration1 20`  // Shutter opening time = 20 seconds (default = 10 seconds).  
    `ShutterCloseDuration1 20` // Shutter closing time = 20 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota.  
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

# 3. One stepper motor (maximum configuration):
### Device List:  
 - Nema-17 (planetary gear motor 1:27).
 - DRV8825 (stepper motor driver).
 - Wemos D1 mini (ESP8266 series wireless board).
 - INA219 (power-monitoring board).
 - MP1584 (DC/DC step-down moduler).

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4111.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4112.jpg)

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file (оr flash your ESP8266 module with `tasmota.bin` file).    
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`   // Enable shutters support.   
    `ShutterMode 4`   // Enable "Shutter mode 4".  
    `Restart 1`   // Restart Tasmota.  
  -  Run commands in the console to configure the motor operation:  
    `ShutterFrequency 2500`    // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 2.5`   // Aacceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration1 20`  // Opening time = 20 seconds (default = 10 seconds).  
    `ShutterCloseDuration1 20` // Closing time = 20 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota.  
  -  Run commands in the consolee to test the motor operation (you must first configure the GPIO!):      
    `ShutterOpen1`   // Opening check.    
    `ShutterStop1`   // Stop check.    
    `ShutterClose1`  // Closing check.  
  -  Perform the [shutter calibration](Blinds-and-Shutters.md#calibration) (Optional).
  -  Run commands in the consolee for configuring the drive (optional):  
    `SetOption73 1`   // Enable detach buttons from relays.  
    `Rule1 ON system#boot DO Backlog SetOption1 1; SetOption11 0; SetOption13 1 ENDON`  
    `Rule2 1`   // Enable Rule1.  
    `Rule2 ON button1#state DO ShutterOpen1 ENDON ON button2#state DO ShutterClose1 ENDON`  
    `Rule2 1`   // Enable Rule2.  
    `Rule3 ON INA219#Current>0.500 DO ShutterStop1 ENDON`  
    `Rule3 1`   // Enable Rule3.  

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


# 4. Two stepper motors (medium configuration):
### Device List:
 - Nema-17 (stepper motor).
 - TMC2208 (stepper motor driver).
 - Wemos D1 mini (ESP8266 series wireless board).
 - MP1584 (DC/DC step-down module).

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4121.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4122.jpg)

### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file (оr flash your ESP8266 module with `tasmota.bin` file).    
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`    // Enable shutters support.   
    `ShutterMode 4`    // Enable "Shutter mode 4".  
    `ShutterRelay1 1`  // for relay Relay1 and Relay2.  
    `ShutterRelay2 3`  // for relay Relay3 and Relay4.    
    `Restart 1`   // Restart Tasmota.  
  -  Run commands in the console to configure the motor operation (you must first configure the GPIO!):  
    `ShutterFrequency 2000`    // This is a global variable for all steppers (default = 1000ppm).  
    `ShutterMotorDelay1 1.5`   // Shutter#1 acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration1 15`  // Shutter#1 opening time = 15 seconds (default = 10 seconds).  
    `ShutterCloseDuration1 15` // Shutter#1 closing time = 15 seconds (default = 10 seconds).  
    `ShutterMotorDelay2 1.5`   // Shutter#2 acceleration/deceleration speed for stepper motor(default = 0 seconds).  
    `ShutterOpenDuration2 15`  // Shutter#2 opening time = 15 seconds (default = 10 seconds).  
    `ShutterCloseDuration2 15` // Shutter#2 closing time = 15 seconds (default = 10 seconds).  
    `Restart 1`   // Restart Tasmota.  
  -  Run commands in the consolee to test the motor operation (you must first configure the GPIO!):      
    `ShutterOpen1`   // Opening check (Shutter#1).    
    `ShutterStop1`   // Stop check (Shutter#1).    
    `ShutterClose1`  // Closing check (Shutter#1).  
    `ShutterOpen2`   // Opening check (Shutter#2).    
    `ShutterStop2`   // Stop check (Shutter#2).    
    `ShutterClose2`  // Closing check (Shutter#2).
  -  Perform the [shutter calibration](Blinds-and-Shutters.md#calibration) (Optional).
  -  Run commands in the consolee for configuring the drive:  
    `SetOption73 1`   // Enable detach buttons from relays.  
    `ShutterButton1 1 updown 0`  // Assigns button1 to act as an "up and down" button (1x press up, 2x press down) for Shutter#1.   
    `ShutterButton2 2 updown 0`  // Assigns button2 to act as an "up and down" button (1x press up, 2x press down) for Shutter#2.  

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

# 4.1 Two stepper motors (medium parallel configuration):  
### Device List:  
 - Nema-17 (stepper motor).  
 - TMC2208 (stepper motor driver).  
 - Wemos D1 mini (ESP8266 series wireless board).  
 - Stepper motor parallel board.  
 - Mini560 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4161.jpg)

# 4.2 Four stepper motors (maximum parallel configuration):  
### Device List:  
 - Nema-17 (stepper motor).  
 - TMC2208 (stepper motor driver).  
 - Wemos D1 mini (ESP8266 series wireless board).  
 - Stepper motor parallel board.  
 - Mini560 (DC/DC step-down module).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/4162.jpg)

# 4. Changing the interface (Optional):  

- By default, `SetOption15` is **ON** and you see three unused components. To hide unused components, run the `SetOption15 OFF` command in the console.  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/SO15.jpg)  

- You can change the labels on the control buttons. Run commands in the console.  

`Backlog WebButton1 &#8648; WebButton2 &#8650`
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/01.jpg) 

`Backlog WebButton1 &#8634; WebButton2 &#8635`
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/02.jpg) 

- To return to the default interface. Run command in the console.  
`Backlog WebButton1 ▲; WebButton2 ▼`


# 6. Components for creating devices (Optional):   

### To customize your devices you can use:  
1. Stepper motor board.  
  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/11.jpg)  
https://aliexpress.com/item/4000393299508.html  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/12.jpg)   
https://aliexpress.com/item/32870732179.html  
https://aliexpress.com/item/33055392128.html  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/21.jpg)  
https://aliexpress.com/item/32905538087.html  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/31.jpg)  
https://aliexpress.com/item/1000007369401.html  

2. Stepper motor parallel board.  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/41.jpg) 
https://aliexpress.com/item/33019883744.html  

3. Stepper motor cable.  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Stepper%20motor/51.jpg) 
https://aliexpress.com/item/32769553792.html  
https://aliexpress.com/item/32811275446.html  

08/28/2021 Added new information, minor bugs fixed.

**Best regards,   
TrDA**  
