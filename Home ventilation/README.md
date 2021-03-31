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

## How to use it:
1. Run commands in the console for ESP-01S (remove comments first):  
  `Rule1`  
  `ON Tele-ENERGY#Current>0.5 DO publish cmnd/Motor-1/Power1 0 ENDON`   // if motor#2 is ON, then turn OFF motor#1  
  `ON Tele-ENERGY#Current<0.5 DO Backlog publish cmnd/Motor-1/Power1 1; publish cmnd/Motor-1/Dimmer 25 ENDON`   // if motor # 2 is OFF, then turn on motor#1 and set motor#1 dimming to 25%  
  `Rule1 1`   // Enable Rule1  

1. Run commands in the console for ESP-01S (remove comments first):  
  `Rule1`  
  `ON system#boot DO Backlog Power1 0; delay 10; Power1 1; Dimmer 25 ENDON`  //turn on motor#2 and set motor#2 dimming to 25%  
  `Rule1 1`   // Enable Rule1  
  `Rule2`  
  `ON Dimmer#State>80 DO Dimmer 25 ENDON`  //turn on motor#2 and set motor#2 dimming to 25%  
  `Rule1 1`   // Enable Rule1  
 
