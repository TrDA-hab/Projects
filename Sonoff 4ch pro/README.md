### How to use it:  
 - You must add support for Shutter in `my_user_config.h` file (оr flash your ESP8266 module with `tasmota.bin` file).  
 - Run commands in the console to run the "Shutter" mode (you must first configure the GPIO!):  
    `SetOption80 1`     // Enable shutters support.   
    `ShutterMode 1`     // Enable "Shutter mode 1".  
    `Restart 1`         // Restart Tasmota.  
    `Interlock 1,2 3,4` //Group Relay1 and Relay2 in "group 1" and Relay3 and Relay4 in "group 2".  
    `Interlock 1`       //Enable relay interlock .  
    `ShutterRelay1 1`   //Set for relay Relay1 and Relay2.
    `ShutterRelay2 3`   //Set for relay Relay3 and Relay4.
-  Run commands in the console to tast and configure the motor operation: 
   `ShutterOpen1` // Engage the relay to open the shutter1.
   `ShutterClose1` // Engage the relay to close the shutter1.
   `ShutterOpenDuration1 5` //Time, in seconds, it takes to fully open the shutter1.
   `ShutterCloseDuration1 5` // Time, in seconds, it takes to fully close the shutter1.
   `ShutterOpen2` // Engage the relay to open the shutter2.
   `ShutterClose2` // Engage the relay to close the shutter2.
   `ShutterOpenDuration2 8` //Time, in seconds, it takes to fully open the shutter2.
   `ShutterCloseDuration2 8` // Time, in seconds, it takes to fully close the shutter2.   

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Sonoff%204ch%20pro/14-1-1.jpg) 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Sonoff%204ch%20pro/14-1-2.jpg) 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Sonoff%204ch%20pro/14-1-3.jpg) 
