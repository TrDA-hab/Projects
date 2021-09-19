## 0. About using I2C multi display.   
 - [How to use I2C bus](https://github.com/arendst/Tasmota/discussions/10827).  
 - [Adafruit info about using 74HC138](https://learn.adafruit.com/delorean-time-circuit/circuit-trickery).
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - Tasmota has [announced](https://github.com/arendst/Tasmota/pull/11821) built-in support for multi-displays but there is no instruction on how it works today 09/18/2021. 
 - You can use any I2C display (only if supported by Tasmota).
 - You can connect a maximum of 3 I2C displays.
 - You can only send information to one display currently active (including the corresponding relay).  
 - The display backlight can only be controlled on the active display. The inactive display saves the display subgrid state.  

## 1. I2C multi display.
### 1.1. Minimal cjofiguration.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4161.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4162.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210918_152007.jpg)   

### 1.2. Miximal cjofiguration.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4171.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4172.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210918_152007.jpg)  

#### Video of the display`s work:   
https://youtu.be/zgQKJD9gmQw   

## 2. How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - **Caution: Displays must be initialized every time the ESP8266 is powered off/on.**
 - To initialize the displays, run the commands in the console:  
   `Power4 1` // To initialize display # 3  
   `Restart 1`  
   `Power2 1` // To initialize display # 2  
   `Restart 1`  
   `Power1 2` // To initialize display # 1  
   `Restart 1`  
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `Interlock 1,2,3` // Group Relay1 and Relay2 and Relay3 in "group 1".  
   `Interlock 1`     // Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton1 LCD#1; WebButton2 LCD#2; WebButton3 LCD#3; WebButton4 Light`  
 - Run the commands in the console to test displays:  
    `Backlog Power4 0; Power1 1; Power4 1` // For run display#1  
    `Backlog Power4 0; Power2 1; Power4 1` // For run display#2  
    `Backlog Power4 0; Power3 1; Power4 1` // For run display#3  

Wemos Pin|GPIO|Component|I2C display|Сomment|
:-:|:-:|:-:|:-:|:-:
D1|05|I2C SCL|SCL|-
D2|12|I2C SDA|SDA|-
D3|00|Relay_1|-|On/Off display#1
D4|02|Relay_2|-|On/Off display#2
D5|14|Relay_3|-|On/Off display#3
D6|12|Relay_4|backligh|On/Off backlight

**Best regards,   
TrDA.**
