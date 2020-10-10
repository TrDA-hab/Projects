
### using Servo Motor 120°/180°/270° (Servo)
Servo controlled by PWM pulses. The angle to which the servo should be set is regulated by the pulse width.  
To operate a servo requires signal uses EN (enable) and PLS (Pulse) for controls rotation angl. 

The servo has no direction of rotation (clockwise or counterclockwise), but only the rotation angle of the output shaft. `Relay2` only shows the direction of rotation - `DIR` (direction), but does not control it. Supports a maximum of four shutters simultaneously with one servo per shutter.  

More information about servo control can be read in [wikipedia](https://en.wikipedia.org/wiki/Servo_control) 

#### Example configuration  
`EN` and `DIR` are on `Relay1` and `Relay2` respectively. Remember to use a **non-inverse relay** for the enable signal.
The `PLS` signal is assigned as a `PWM<x>` component where `<x>` matches the number of the shutter (e.g., `PWM1` for `Shutter1`).

The PWM frequency must be set with the `PWMfrequency 200` command. The frequency setting is a global setting all PWM components on the device. This means that all shutters on the device will operate at the same speed.

Using the `ShutterMotorDelay` command to provide a slow increase / decrease in speed. This causes the driver to ramp the speed up and down during the defined duration. The change of the ShutterMotorDelay does NOT change the distance the shutter makes. This is very convinent to trim the accelerate and decelerate rate without changeing the distance.

`ShutterOpenDuration` and `ShutterCloseDuration` define the open / close time. By changing the times you adjust the speed of the servo output shaft. `ShutterOpenDuration` and `ShutterCloseDuration` can be different.

Using the `ShutterPwmRange` command to set the pulse width range:
 - position 0° pulse width 500...1000ms.
 - position 90° pulse width ~1500ms (center position is calculated automatically).
 - position 180° pulse width 2000...2500ms.

The calculation of parameters for `ShutterPwmRange` is obtained by dividing by 5 the minimum and maximum values of the pulse width range. 
For example the pulse width range for different servos:
1. Servo mg90s (180°): pulse width range 544 - 2400ms (1520ms center position), `ShutterPwmRange` 109, 480
2. Servo TD-8130MG (180°): pulse width range 500 - 2500ms (1500ms center position), `ShutterPwmRange` 100, 500

!!! note 
    Even within the same servo model, there may be manufacturing tolerances that result in a different operating range of pulse lengths. For accurate operation, each specific servo must be calibrated: through experiments, it is necessary to select the correct range that is specific to it. 

Wemos Pin|GPIO|Component|Servo Signal
:-:|:-:|:-:|:-:
D3|0|Relay1|EN
D4|2|PWM1|PLS
D5|14|Relay2|DIR

**a) Enable Shutters**  
   `SetOption80 1`   // this is a global variable for all Shutters 

**b) Set ShutterMode**  
   `Shuttermode 5`   // enable Shutter mode for servo 

**c) Setting the PWM frequency**  
   `PWMfrequency 200`   // this is a global variable for all Servos  

**d) Set control values**  
   `SetOption15 0`  // to control the storage of values

**e) Set at least a small ramp-up/ramp down period 1.0 second (optional)**  
   `ShutterMotorDelay1 1.0`  // servo does not like abrupt start / stop

**f) Set the pulse width range**  
   `ShutterPwmRange 100, 500`  //this is a global variable for all Servos

**g) Restart Tasmota**  
   `Restart 1`

**h) Test the shutter1**  
   `ShutterOpen1`   
   `ShutterStop1`      // to stop the SERVO1  
   `ShutterClose1`  
   `ShutterInvert1`    // to change the direction of rotation of the SERVO1  

**i) Perform the [shutter calibration](Blinds-and-Shutters.md#calibration)**    

#### Configuration for additional shutters  
You must first set up the first shutter and only then the next.  

Wemos Pin|GPIO|Component|Stepper Signal
:-:|:-:|:-:|:-:
D6|12|Relay3|EN
D7|13|PWM2|PLS
D8|15|Relay4|DIR


**a) Configure Shutter2**  
  `ShutterRelay2 1`   // for relay Relay3 and Relay4  

**b) Restart Tasmota**  
  `Restart 1`

**d) Test the shutter2**  
  `ShutterOpen2`  
  `ShutterStop2`     // to stop the SERVO2  
  `ShutterClose2`  
  `ShutterInvert2`   // to change the direction of rotation of the SERVO2  

**e) Perform the [shutter calibration](Blinds-and-Shutters.md#calibration)**    


#### Motor Wiring Diagrams  
#### One Shutter  
![511](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Servo%2BESP8266/Servo-511.jpg)
- Diagram v512: Minimum configuration for one servo, power on continuously.  
![512](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-512.jpg)
- Diagram v514: Optimal configuration for one servo, power is supplied via the relay only if the servo is running.  
![514](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-514.jpg)
- Diagram v516: Maximum configuration for one servo, power is supplied via relay only if servo is running, operating current control via INA219.  
![516](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-516.jpg)

#### 2 Shutters  
![521](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-521.jpg)
- Diagram v522: Minimum configuration for two servos, power on continuously.  
![522](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-522.jpg)
- Diagram v524: Optimal configuration for two servos, power is supplied through the relay only if the servo is running individually for each servo.  
![524](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-524.jpg)
- Diagram v526: Maximum configuration for two servos, power is supplied via the relay only if the servo is running, control of the operating current via INA219 is individual for each servo.  
![526](https://github.com/TrDA-hab/Projects/raw/master/Servo%2BESP8266/Servo-526.jpg)
