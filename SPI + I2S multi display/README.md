## 0. About using SPI + I2C multi display (software mode).   
 - [WIKI SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface).  
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - Tasmota has [announced](https://github.com/arendst/Tasmota/pull/11821) built-in support for multi-displays but there is no instruction on how it works today 09/17/2021.   
 - You can use any SPI display that uses a 3-wire SPI bus. 4-wire SPI bus - not tested, but should work too (only they are supported by Tasmota).
 - You can connect a maximum of 8 displays using the ESP8266, or more using the ESP32.
 - You can display the same information on all displays at once (by switching on all relays) or display information individually on each display (including the corresponding relay).
 -  Step by step [instructions for E-Paper Display](https://github.com/arendst/Tasmota/discussions/11850).  

## 1. SPI + I2C multi display.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4181.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4182.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4183.jpg)    
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/20210925_203145.jpg)   

#### Video of the display`s work:   
https://youtu.be/MSbM2clI2aU   

## 2. How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - Make all the necessary settings necessary for your display to function.  
 - Run the command in the console  to run the "Interlock" mode, for the possibility of individual output of information on displays (optional):  
   `SetOption73 ON` // Enable detach buttons from relays.  
   `Interlock 1,2,3` //Group Relay1 and Relay2 and Relay3 in "group 1".  
   `Interlock 1`     //Enable relay interlock mode.  
 - Run the command in the console to modify the interface (optional):   
   `Backlog WebButton1 E-PAPER#1; WebButton2 E-PAPER#2; WebButton3 E-PAPER#3`  
 - Run commands in the console for test Display:    
   `Backlog Power1 1; DisplayText [z]`  // For run display#1.  
   `DisplayText [f0s2x2y2tS]`    // Print text on display#1.  
   `Backlog Power2 1; DisplayText [z]`  // For run display#2.  
   `DisplayText [f0s2x2y2tS]`    // Print text on display#2.   
   `Backlog Power3 1; DisplayText [z]`  // For run display#3.  
   `DisplayText [f0s2x2y2tS]`    // Print text on display#3.   

ESP32 GPIO|Component|SPI display|SPI display|
:-:|:-:|:-:|:-:
21|I2C SDA 1|SDA|-
22|I2C SCL 2|SCL|-
13|SSPI MOSI|-|DIN
183|SSPI SCLK|-|CKL
05|EPaper29 CS|-|CS

**Best regards,   
TrDA.**
