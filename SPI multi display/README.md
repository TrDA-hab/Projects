## 0. About using SPI multi display.   
 - You can use any SPI display that uses a 3-wire SPI bus. 4-wire SPI bus - not tested, but should work too.
 - You can connect a maximum of 8 displays using the ESP8266, or more using the ESP32.
 - You can display the same information on all displays at once (by switching on all relays) or display information individually on each display (including the corresponding relay).
 -  Step by step [instructions for E-Paper Display](https://github.com/arendst/Tasmota/discussions/11850).  

## 1. SPI multi display.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4151.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4152.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/20210917_191722.jpg)   

## 2. How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file:    

 - Enter the command in the console to initialize the displays after restarting the ESP8266 (you must first configure the GPIO!):  
   `Rule1 ON system#boot DO Backlog Power2 1; Power3 1; Power4 1; DisplayText [z]; ENDON`  
   `Rule1 1`   // Run Rule1   
 - Run commands in the console for test Display:    
   `Backlog DisplayText [z]; DisplayText [f0s2x2y2tS]`  
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `Interlock 1,2,3` //Group Relay1 and Relay2 and Relay3 in "group 1".  
   `Interlock 1`     //Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton2 E-PAPER#1; WebButton3 E-PAPER#2; WebButton4 E-PAPER#3`  

#### Video of the driver's work:   
https://youtu.be/MSbM2clI2aU   

Wemos Pin|GPIO|Component|SPI display|Сomment|
:-:|:-:|:-:|:-:|:-:
D3|00|Relay_i 3|CS#3|On/Off display#3
D4|02|Relay_i 4|CS#2|On/Off display#2
D5|14|Relay_i 2|CS#1|On/Off display#1
D6|12|SSPI MOSI|DIN|-
D7|13|SSPI SCLK|CKL|-
D8|15|EPaper29 CS|-|virtual pin



**Best regards,   
TrDA.**
