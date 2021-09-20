## 0. About using I2C multi display.   
 - [How to use I2C bus](https://github.com/arendst/Tasmota/discussions/10827).  
 - Adafruit info [about using 74HC138](https://learn.adafruit.com/delorean-time-circuit/circuit-trickery).  
 - 74hc138 [datasheet](https://static.chipdip.ru/lib/935/DOC011935338.pdf).   
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - Tasmota [use Buttons](https://tasmota.github.io/docs/Buttons-and-Switches/#button).   
 - Tasmota [use Rules](https://tasmota.github.io/docs/Rules/).    
 - Tasmota has [announced](https://github.com/arendst/Tasmota/pull/11821) built-in support for multi-displays but there is no instruction on how it works today 09/18/2021. 
 - You can use any I2C display (only if supported by Tasmota). SPI displays have not been tested, but should work too.
 - You can connect x3 I2C displays.  
   - or up to x6 maximum, if you modify the circuit (if you are using ESP8266).  
   - or up to x8 maximum, if you modify the circuit (if you are using ESP32).   
 - You can only send information to one display currently active (including the corresponding relay).  
 - The display backlight can only be controlled on the active display. The inactive display saves the display subgrid state.  
 - **!!!Caution!!!** 
   - Displays must be initialized every time the ESP8266/ESP32 is powered off/on.  
   - After Hardware or Software Reset, all display settings are saved.**  

## 1. I2C multi display (minimal cofiguration).  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4161.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4162.jpg)   

Wemos Pin|GPIO|Component|I2C display|Сomment|
:-:|:-:|:-:|:-:|:-:
D1|05|I2C SCL|SCL|-
D2|12|I2C SDA|SDA|-
D3|00|Relay_1|-|On/Off display#1
D4|02|Relay_2|-|On/Off display#2
D5|14|Relay_3|-|On/Off display#3
N/C|-|Relay_4|backligh|On/Off backlight

## How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - **Caution!!! Displays must be initialized every time the ESP8266 is powered off/on.**
 - To initialize the displays, run the commands in the console:  
   `Backlog Power3 1; Power4 1; Restart 1`  // To initialize display#3 and restart Tasmota.  
   `Backlog Power2 1; Power4 1; Restart 1`  // To initialize display#2 and restart Tasmota.    
   `Backlog Power1 1; Power4 1; Restart 1`  // To initialize display#1 and restart Tasmota.    
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `SetOption73 ON`  // Enable detach buttons from relays.  
   `Interlock 1,2,3` // Group Relay1 and Relay2 and Relay3 in "group 1" (only one display can work at a time).  
   `Interlock 1`     // Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton1 LCD#1; WebButton2 LCD#2; WebButton3 LCD#3; WebButton4 Light`  
 - Run the commands in the console to test displays:  
   `Backlog Power4 0; Power1 1; Power4 1` // For run display#1.  
   `Backlog Power4 0; Power2 1; Power4 1` // For run display#2.  
   `Backlog Power4 0; Power3 1; Power4 1` // For run display#3.  

## 2. I2C multi display (maximal cofiguration).   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4171.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4172.jpg)    

Wemos Pin|GPIO|Component|I2C display|Сomment|
:-:|:-:|:-:|:-:|:-:
D1|05|I2C SCL|SCL|-
D2|12|I2C SDA|SDA|-
D3|00|Relay_1|-|On/Off display#1
D4|02|Relay_2|-|On/Off display#2
D5|14|Relay_3|-|On/Off display#3
N/C|-|Relay_4|backligh|On/Off backlight
TX|01|Button_1|-|Switching between displays
RX|03|Button_2|backligh|On/Off backlight  

## How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - **Caution!!! Displays must be initialized every time the ESP8266 is powered off/on.**
 - To initialize the displays, run the commands in the console:  
   `Backlog Power3 1; Power4 1; Restart 1`  // To initialize display#3 and restart Tasmota.  
   `Backlog Power2 1; Power4 1; Restart 1`  // To initialize display#2 and restart Tasmota.  
   `Backlog Power1 1; Power4 1; Restart 1`  // To initialize display#3 and restart Tasmota.  
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `SetOption73 ON`  // Enable detach buttons from relays.  
   `Interlock 1,2,3` // Group Relay1 and Relay2 and Relay3 in "group 1" (only one display can work at a time).  
   `Interlock 1`     // Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton1 LCD#1; WebButton2 LCD#2; WebButton3 LCD#3; WebButton4 Light`  
 - Run the commands in the console to test displays:  
   `Backlog Power4 0; Power1 1; Power4 1` // For run display#1.  
   `Backlog Power4 0; Power2 1; Power4 1` // For run display#2.  
   `Backlog Power4 0; Power3 1; Power4 1` // For run display#3.  
 - Assigns button#1 to Switching between displays (1x press up, 2x press down, 3x press down):
   `Rule1` 
   `ON button2#state=10 DO Backlog Power4 0; Power1 1; Power4 1 ENDON`  // 1x press up to run display#1.    
   `ON button2#state=11 DO Backlog Power4 0; Power2 1; Power4 1 ENDON`  // 3x press up to run display#2.      
   `ON button2#state=12 DO Backlog Power4 0; Power3 1; Power4 1 ENDON`  // 3x press up to run display#5.      
   `Rule1 1`  // Enable Rule1.  
 - Assigns button#2 to On/Off Display backlight (1x press up, 2x press down):   
   `Rule2`   
   `ON button1#state=10 DO Power4 0 ENDON`  // 1x press up to OFF Display backlight.  
   `ON button1#state=11 DO Power4 1 ENDON`  // 2x press up to ON Display backlight.  
   `Rule2 1` // Enable Rule2.  

## 3. Practical use.  
### Video of the display`s work:   
 - [Video#1](https://youtu.be/zgQKJD9gmQw).   
 - [Video#2](https://youtu.be/Cm0D1HlTeSg).  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210919_193223.jpg) 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210918_152007.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210919_192536.jpg)  

**Best regards,   
TrDA.**
