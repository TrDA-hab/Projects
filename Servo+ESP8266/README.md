## Using Servo Motor

Servo controlled by PWM pulses. The angle to which the servo should be set is regulated by the pulse width.  
The servo has no direction of rotation (clockwise or counterclockwise), but only the rotation angle of the output shaft. 

To operate a servo requires signal uses:

-  `EN` (enable) turn on / off servo.
-  `PLS` (pulse) for controls rotation angl.
-  `DIR` (direction) only shows the direction of rotation, but does not control it. 

## More information:
 - [About shutter](https://tasmota.github.io/docs/Blinds-and-Shutters/)
 - [Shutter commands](https://tasmota.github.io/docs/Commands/#shutters)
 - [Wikipedia](https://en.wikipedia.org/wiki/Servo_control) 
 - [How to Mod a Servo to Get Closed Loop Feedback](https://github.com/arendst/Tasmota/discussions/10387)
 - [as5600 + Servo motor](https://hackaday.io/project/17079-mocoder-magnetic-encoder)


## Example configuration  
`EN` and `DIR` are on `Relay1` and `Relay2` respectively. Remember to use a **non-inverse relay** for the enable signal.
The `PLS` signal is assigned as a `PWM<x>` component where `<x>` matches the number of the shutter (e.g., `PWM1` for `Shutter1`).

The PWM frequency must be set with the `PWMfrequency 200` command. The frequency setting is a global setting all PWM components on the device. This means that all shutters on the device will operate at the same speed.

Using the `ShutterMotorDelay` command to provide a slow increase / decrease in speed. This causes the driver to ramp the speed up and down during the defined duration. The change of the ShutterMotorDelay does NOT change the distance the shutter makes. This is very convinent to trim the accelerate and decelerate rate without changeing the distance.

`ShutterOpenDuration` and `ShutterCloseDuration` define the open / close time. By changing the times you adjust the speed of the servo output shaft. `ShutterOpenDuration` and `ShutterCloseDuration` can be different.

Using the `ShutterPwmRange` command to set the pulse width range. The calculation of parameters for `ShutterPwmRange` is obtained by dividing by 5 the minimum and maximum values of the pulse width range. 

## Note!
Even within the same servo model, there may be manufacturing tolerances that result in a different operating range of pulse lengths. For accurate operation, each specific servo must be calibrated: through experiments, it is necessary to select the correct range that is specific to it. 

For example the pulse width range for different servos:

-  Servo MG90 (180°): pulse width range 544 - 2400ms, `ShutterPwmRange` 109, 480
-  Servo TD-8130MG (180°): pulse width range 500 - 2500ms, `ShutterPwmRange` 100, 500

## Servo datasheet:
-  [Servo MG90](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/MG90S-Datasheet.pdf)
-  [Servo TD-8130MG](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/TD-8130MG.jpg)
-  [Servo DS5160ssg](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/DS5160ssg.jpg)

Wemos Pin|GPIO|Component|Servo Signal
:-:|:-:|:-:|:-:
D3|0|Relay1|EN
D4|2|PWM1|PLS
D5|14|Relay2|DIR

## How to use it:
- You must add support for Shutter in my_user_config.h file (оr flash your ESP8266 module with tasmota.bin file).
- Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
   `SetOption80 1`     // enable Shutters support.  
   `Shuttermode 5`     // enable Shutter mode for servo.  
   `PWMfrequency 200`  // this is a global variable for all Servos.  
   `SetOption15 0`     // to control the storage of values.  
   
- Run commands in the console to configure the motor operation:   
   `ShutterPwmRange1 100, 500`  //this is a global variable for all Servos.  
   `ShutterOpenDuration1 0.5`   // define the open time, in seconds.  
   `ShutterCloseDuration1 0.5`  // define the close time, in seconds.   
   `ShutterMotorDelay1 0.2`     // servo does not like abrupt start / stop.  
   `Restart 1`  
- Run commands in the consolee to test the motor operation:   
   `ShutterOpen1`      // to open the SERVO#1.   
   `ShutterStop1`      // to stop the SERVO#1.   
   `ShutterClose1`     // to close the SERVO#1.  
   
- Perform the [shutter calibration](https://tasmota.github.io/docs/Blinds-and-Shutters/#calibration)  (optional).   

## Motor Wiring Diagrams  
### One Shutter  
![511](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/511.jpg)
- Diagram v512: Minimum configuration for one servo, power on continuously.  
![512](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/512.jpg)

### Dual Shutter  
![521](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/521.jpg)
- Diagram v522: Optimal configuration for two servos, power is supplied through the relay.  
![522](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/522.jpg)
- Diagram v532: Maximum configuration for two servos, power is supplied via the relay only if the servo is running. Current control for each servo drive via INA219.
![532](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/532.jpg)

## Additional Information:
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/Servo-2%20v8.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/Servo1%20v12.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/20210106_171232.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/20210106_171217.jpg)

##Best regards  
TrDA##
