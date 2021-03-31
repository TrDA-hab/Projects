# Home ventilation (automation). 

## 1. RobotDyn AC Light Dimmer.  
 - this only works if your AC motor is dimmable.
 - it hums a lot when running (low frequency hum).
 - this is unacceptable (work stopped).

![RobotDyn Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/PZEM-852.jpg)

## 2. Sonoff D1 Dimmer.  
 - this only works if your AC motor is dimmable.
 - it works very well (almost).
 
![RobotDyn Dimmer](https://raw.githubusercontent.com/TrDA-hab/Projects/master/Home%20ventilation/PZEM-862.jpg)

## More about using PZEM-004:
 - [Tasmota PZEM-004](https://tasmota.github.io/docs/PZEM-0XX/)
 - [about using PZEM-004](https://github.com/arendst/Tasmota/discussions/10567)

 ## How to use it (for ESP-01S):
1. Run commands in the console to reset values:
 - `EnergyReset1 0`   // reset values for Today  
 - `EnergyReset2 0`   // reset values for Yesterday  
 - `EnergyReset3 0`   // reset values for Total 

