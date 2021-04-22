## 0.  About SPI E-Ink Display:
- Tasmota E-Paper support [1](https://tasmota.github.io/docs/Displays/#notes-on-e-paper-displays), [2](https://tasmota.github.io/docs/Displays/#hardware-connections).
- Tasmota currently (2021-04-21) only supports two E-Ink displays from the **Waveshare** manufacturer: 2.9inch (black, white) and 4.2inch (black, white): [1](https://www.waveshare.com/2.9inch-e-paper-module.htm), [2](https://www.waveshare.com/4.2inch-e-Paper-Module.htm).
- **Waveshare** has produced three versions of the 2.9inch e-Paper display at different times: Rev1.0, Rev2.0, Rev2.1.
- **Waveshare** 2.9inch e-Paper display Rev1.0.
  - [Schematic](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V10/20181015111121!2.9inch_e-Paper_Schematic.pdf).
  - [User manual](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V21/2.9inch-e-paper-module-user-manual-en.pdf). 
- **Waveshare** 2.9inch e-Paper display Rev2.0.
  - [Schematic](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V20/20200103064632!2.9inch_e-Paper_Schematic.pdf).
  - [Datasheet](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V20/20200331114041!2.9inch_e-Paper_Datasheet.pdf).
  - [User manual](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V21/2.9inch-e-paper-module-user-manual-en.pdf). 
- **Waveshare** 2.9inch e-Paper display Rev2.1.
  - [Schematic](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V21/2.9inch_e-Paper_Schematic.pdf).
  - [Datasheet](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V20/20200103064632!2.9inch_e-Paper_Schematic.pdf).
  - [User manual](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V21/2.9inch-e-paper-module-user-manual-en.pdf). 
  - [Specificationl](https://github.com/TrDA-hab/Projects/blob/master/E-PAPER/V21/2.9inch-e-paper-v2-specification.pdf).  
 
 ![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/20210422_095444.jpg)

## 1. **Waveshare** 2.9inch e-Paper display (simple configuration).

![4.12.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/4121.jpg)
![4.12.2](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/4122.jpg) 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/20210422_100745.jpg)

Wemos Pin|GPIO|Component|e-Paperl
:-:|:-:|:-:|:-:
D5|14|EPaper29 CS|CS
D6|12|SSPI MOSI|DIN
D7|13|SSPI SCLK|CKL


## 2. **Waveshare** 2.9inch e-Paper display (medium configuration).
![4.12.3](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/4123.jpg)
![4.12.4](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/4124.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/20210422_100745.jpg)   

Wemos Pin|GPIO|Component|e-Paperl
:-:|:-:|:-:|:-:
D5|14|EPaper29 CS|CS
D6|12|SSPI MOSI|DIN
D7|13|SSPI SCLK|CKL
D1|5|I2C SCL|-
D2|4|I2C SDA|-

## 3. Practical use.
### How to use it:  
 - You must add support for "2.9inch e-Paper display" in `my_user_config.h` file #define `USE_SPI`, `#define USE_DISPLAY`, `#define USE_DISPLAY_EPAPER29`.
 - Or flash our ESP8266 module with `tasmota-display.bin` file.
 - If you have done all the necessary settings and connections correctly, then after starting (or restarting) the ESP you will see all the found e-Paper display.   .  
  `00:00:00.058 SPI: Software using GPIO13(CLK) and GPIO12(MOSI)`  
  `00:00:00.024 DSP: E-Paper 2.9`  
 - To check, enter the `display` command in the console, you should see the response:   
  `21:11:28.863 RSL: stat/tasmota_302886/RESULT = {"Display":{"Model":5,"Width":128,"Height":296,"Mode":0,"Dimmer":1,"Size":1,"Font":2,"Rotate":1,"Refresh":2,"Cols":[16,8],"Rows":2}}`  


![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/20210422_095345.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/E-PAPER/20210422_101451.jpg)
