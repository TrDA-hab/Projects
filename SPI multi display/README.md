## 0. About using SPI multi display.   
 - [WIKI SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface).  
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - Tasmota [use Buttons](https://tasmota.github.io/docs/Buttons-and-Switches/#button).   
 - Tasmota [use Rules](https://tasmota.github.io/docs/Rules/).    
 - Step by step [instructions for E-Paper Display](https://github.com/arendst/Tasmota/discussions/11850).  
 - You can use any SPI display that uses a 3-wire SPI bus. 4-wire SPI bus - not tested, but should work too (only they are supported by Tasmota).
 - You can connect a maximum of 8 displays using the ESP8266, or more using the ESP32.  
 - You can:  
   - display the same information on all displays at once (by switching on all relays);  
   - or display information individually on each display (including the corresponding relay);  
   - or use mirror display.  

## Other projects where multi display is used:
 - Tasmota [I2C multi display (hardware mode)](https://github.com/arendst/Tasmota/discussions/13166).  
 - Tasmota [SPI+I2C multi display (software mode)](https://github.com/arendst/Tasmota/discussions/13222).  
 - [ESP32 and 8 OLEDs arranged in a circle](https://youtu.be/KZTIBoHtouM). 
 - [Multiple displays on the I2C bus](https://www.youtube.com/watch?v=E9FTQyBYwAE).  
 - [8 Multiplexed OLED /w ESP32 and U8g2](https://www.youtube.com/watch?v=aMgIxXwtHbw).  
 - [SPI OLED multiple displays with an Arduino](https://youtu.be/YCkFFtVEEG4).  
 - [Multiple SPI based Displays with TFT_eSPI on an esp32](https://youtu.be/cCgNHIHijhs).  
 - [Multiple Displays with Arduino](https://youtu.be/yef23sJjiU0).  
 - [Multiple OLED screens](https://youtu.be/TOMkXJWdB4w).  
 - [Multiple OLED Displays / Multiplex TC9548](https://youtu.be/Y9OyLMUgoFk).  

## 1. SPI mirror display (minimal configuration).
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4191.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4192.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/20210927_164541.jpg) 

## How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - Make all the necessary settings for your display to function.  
 - Run commands in the console for test mirror Display:    
  `Backlog DisplayText [z]; DisplayText [f0s2x2y2tS]; DisplayText [f0s2x2y22tS]; DisplayText [f0s2x2y42tS];`  
  `DisplayText [f0s2x2y62tS]; DisplayText [f0s2x2y82tS]; DisplayText [f0s2x2y102tS]; DisplayText [f0s2x2y122tS];`  
  `DisplayText [f0s2x2y142tS]; DisplayText [f0s2x2y162tS]; DisplayText [f0s2x2y182tS]; DisplayText [f0s2x2y202tS];`  
  `DisplayText [f0s2x2y222tS]; DisplayText [f0s2x2y242tS]; DisplayText [f0s2x2y262tS]; DisplayText [f0s2x2y282tS]`  

Wemos Pin|GPIO|Component|SPI display|
:-:|:-:|:-:|:-:
D5|14|EPaper29 CS|CS
D6|12|SSPI MOSI|DIN
D7|13|SSPI SCLK|CKL

## 2. SPI multi display (medium configuration).

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4151.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4152.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/20210917_191722.jpg)   

#### Video of the display`s work:   
https://youtu.be/MSbM2clI2aU   

## How to use it.  
 - You must add support for display in `my_user_config.h` file, or flash our ESP8266 module with `tasmota-display.bin` file.   
 - Make all the necessary settings for your display to function.  
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

Wemos Pin|GPIO|Component|SPI display|Сomment|
:-:|:-:|:-:|:-:|:-:
D3|00|Relay_i 1|SS#1|On/Off display#1
D4|02|Relay_i 2|SS#2|On/Off display#2
D5|14|Relay_i 3|SS#3|On/Off display#3
D6|12|SSPI MOSI|DIN|-
D7|13|SSPI SCLK|CKL|-
D8|15|EPaper29 CS|-|virtual pin

## 3. SPI multi display (maximum configuration).

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20multi%20display/4202.jpg)

**Best regards,   
TrDA.**
