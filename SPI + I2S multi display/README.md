## 0. About using SPI + I2C multi display (software mode).   
 - [WIKI SPI](https://en.wikipedia.org/wiki/Serial_Peripheral_Interface).  
 - Step by step [instructions for E-Paper Display](https://github.com/arendst/Tasmota/discussions/11850).  
 - Tasmota [commands](https://tasmota.github.io/docs/Commands/#displays) for controlling displays.  
 - Tasmota [examples](https://tasmota.github.io/docs/Displays/#rule-examples-for-scripting-examples-see-scripting-docs) for displaying information on the display.  
 - You can display the same information on all displays at once or display information individually on each display.

## Other projects where multi display is used:
 - Tasmota [SPI multi display (hardware mode)](https://github.com/arendst/Tasmota/discussions/13161).  
 - Tasmota [I2C multi display (hardware mode)](https://github.com/arendst/Tasmota/discussions/13166).  
 - [ESP32 and 8 OLEDs arranged in a circle](https://youtu.be/KZTIBoHtouM). 
 - [Multiple displays on the I2C bus](https://www.youtube.com/watch?v=E9FTQyBYwAE).  
 - [8 Multiplexed OLED /w ESP32 and U8g2](https://www.youtube.com/watch?v=aMgIxXwtHbw).  
 - [SPI OLED multiple displays with an Arduino](https://youtu.be/YCkFFtVEEG4).  
 - [Multiple SPI based Displays with TFT_eSPI on an esp32](https://youtu.be/cCgNHIHijhs).  
 - [Multiple Displays with Arduino](https://youtu.be/yef23sJjiU0).  
 - [Multiple OLED screens](https://youtu.be/TOMkXJWdB4w).  
 - [Multiple OLED Displays / Multiplex TC9548](https://youtu.be/Y9OyLMUgoFk).  

## 1. ESP32 + E-Papper (slot 1) + SSD1306 (slot 2).
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4181.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4182.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/20210929_193251.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/20210925_203145.jpg)   

### How to use it.  
#### Video of the display`s work:   
https://youtu.be/DtdU9AR7CBk   

ESP32 GPIO|Component|I2C display|SPI display|
:-:|:-:|:-:|:-:
21|I2C SDA 1|SDA|-
22|I2C SCL 2|SCL|-
13|SSPI MOSI|-|DIN
18|SSPI SCLK|-|CKL
05|EPaper29 CS|-|CS

 - very soon !!!  
 - 
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/001.jpg)    
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/002.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/003.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/004.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/005.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/006.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/007.jpg)     

```arduino
>B
; load SD1306 driver on boot
dt [S2/SD1306_display.ini:]
; clear screen, switch to LCD font; set auto draw
dt [zf1s1D1]
; switch to display 1
dt [S1:]
>S
; switch to display 2
dt [S2:]
; show time
dt [x35y30tS]
; switch back to display 1
dt [S1:]
; show time
dt [x10y10tS]
```

## 2. Other variants that have been tested (09/30/2021).  

**!!! Attention: !!! the multi-display software mode is currently in testing mode.**
- `ESP32 + E-Papper (slot 1) + SSD1306 (slot 2)` = works well.
- `ESP32 + LCD1602 (slot 1) + SSD1306 (slot 2)` = works well.
- `ESP8266 + ILI9341 (slot 1) + SH1106 (slot 2)` = works well (info from gemu2015).
- `ESP32 + LCD1602 (slot 1) + SH1106 (slot 2) + ILI9341 (slot 3)` = works well (info from gemu2015).
- `ESP32 + SSD1306 (slot 1) + E-Papper (slot 2)` = more tests needed.
- `ESP32 + E-Papper (slot 1) + E-Papper (slot 2)` = more tests needed.

**!!! For your information only !!!**

### 2.1 ESP32 + E-Papper (slot 1) + SSD1306 (slot 2) + BME280.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4183.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/4184.jpg)   
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/20211001_201308.jpg)   
```arduino
>D
hum=0
temp=0
press=0
>B
; load SD1306 driver on boot
dt [S2/SD1306_display.ini:]
; clear screen, switch to LCD font; set auto draw
dt [zf1s1D1]
; switch to display 1
dt [S1:]
>S
; switch to display 2
dt [S2:]
; show time
dt [x35y30tS]
; switch back to display 1
dt [S1:]
dt [x10y10tS]
; update display every TelePeriod
if upsecs%tper==0
then
dp2
dt [x10y40]%temp% C
dt [x10y60]%hum% %%
dt [x10y80]%press% mmHg
dt [d]
endif
>T
; get some telemetry values
hum=BME280#Humidity
temp=BME280#Temperature
press=BME280#Pressure 
```

### 2.2 ESP32 + LCD1602 (slot 1) + SSD1306 (slot 2).
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/SPI%20%2B%20I2S%20multi%20display/20210930_192427.jpg)   
```arduino
>B
; load SD1306 driver on boot
dt [S2/SD1306_display.ini:]
; clear screen, switch to LCD font; set auto draw
dt [zf1s1D1]
; switch to display 1
dt [S1:]
>S
; switch to display 2
dt [S2:]
; show time
dt [x35y30tS]
; switch back to display 1
dt [S1:]
; show time
dt [x0y0tS]
```

**Best regards,   
TrDA.**
