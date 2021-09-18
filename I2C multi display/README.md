## 0. About using SPI multi display.   
 - [How to use I2C bus](https://github.com/arendst/Tasmota/discussions/10827).  
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - Tasmota has [announced](https://github.com/arendst/Tasmota/pull/11821) built-in support for multi-displays but there is no instruction on how it works today 09/17/2021.   
 - You can use any I2CI display (only they are supported by Tasmota).
 - You can connect a maximum of 3 I2C displays using.
 - You can display the same information on all displays at once (by switching on all relays) or display information individually on each display (including the corresponding relay).
 - The display illumination can be controlled on the active display. The inactive display saves the display subgrid state.  

## 1. I2C multi display.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4161.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/4161.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20multi%20display/20210918_152007.jpg)   

#### Video of the display`s work:   
https://youtu.be/zgQKJD9gmQw   

## 2. How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `Interlock 1, 2,3` //Group Relay1 in "group 1" and Relay2 and Relay3 in "group 2".  
   `Interlock 1`     //Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton2 LCD#1; WebButton3 LCD#2; WebButton4 LCD#3; WebButton5 Light`  
 - Run the command in the console to test display`s:
    `Backlog Power5 0; Power2 1;Power5 1` // For run display#1  
    `Backlog Power5 0; Power3 1;Power5 1` // For run display#2  
    `Backlog Power5 0; Power4 1;Power5 1` // For run display#3  

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
