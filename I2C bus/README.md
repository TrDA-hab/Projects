## About I²C (I2C, IIC) bus:
- [Tasmota - Supported I²C devices](https://tasmota.github.io/docs/I2CDevices/#supported-i2c-devices)
- [Wikipedia](https://en.wikipedia.org/wiki/I%C2%B2C)  
- [Sparkfun - I²C Bus tutorial](https://learn.sparkfun.com/tutorials/i2c)  
- [NodeMCU - I²C Bus tutorial](https://nodemcu.readthedocs.io/en/release/modules/i2c/)  
- [Wemos - pin map](https://nodemcu.readthedocs.io/en/release/modules/i2c/)
- [NXP - I²C bus specification](https://www.nxp.com/docs/en/user-guide/UM10204.pdf)
- [TI - I²C Bus Pull-up resistor calculation](https://www.ti.com/lit/an/slva689/slva689.pdf)
- [Online - I²C Bus Pull-up resistor calculator](https://atman-iot.com/blog/i2c-pull-up-calculator/)

## 0. 
**About using the I²C bus:**
- the maximum allowable I²C bus capacitance is 400 pF, the bus length does NOT matter.
- it is not allowed to use devices with the same addresses.
- the maximum number of devices on the I²C bus is no more than 128 pcs. Addresses from 0 to 127, one for "master" and others for "slave". Excluding reserved addresses ([1](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#1)).
- ready-made I²C modules, already have pull-up resistors, and you should not worry.
- what type of pull-up resistors should we choose for "handmade" device? It depends on many factors, but to be on the safe side anything between 1.5 kΩ and 14 kΩ (optimal 4.7 kΩ). The more devices are connected to the I²C bus the smaller(!) has to be the resistor.
- the ESP8266(ESP32) activates its internal pull-up resistors for SDA and SCL, so you usually don't need to install external ones (they are required for slaves).
- if you need a "longer" I²C bus, you must use a repeater ([2](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#2)).  
- if you need more devices with the same address, you must use a multiplexer ([3](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#3)).  
- if it is necessary to logically match the levels, you must use alevel translator ([4](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#4)).
- if you need to connect several sensors, you must use I²C extender ([5](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#5)).
- I²C bus allows connecting ([hot-swappable](https://www.ti.com/lit/an/scpa058/scpa058.pdf)) modules.
- for the I²C bus, you can use the ([Rx and Tx](https://tasmota.github.io/docs/devices/Sonoff-Basic-and-BME280/#connect-bme280-to-sonoff-basic-based-on-the-gpio-locations)) of your ESP8266. 
- the ESP8266 chip does not have hardware I²C, so module uses software I²C driver. It can be set up on any GPIO pins. The recommended convention for the I²C bus is used to select the GPIO pins - `SDA` on GPIO4 (D2) and  `SCL` on GPIO5 (D1). For ESP32 recommend using GPIO pins - `SDA` on GPIO21 and` SCL` on GPIO22.
- if you have done all the necessary settings and connections correctly, then after starting (or restarting) the ESP you will see all the found I²C devices.   
  `00:00:03.974 I2C: BME280 found at 0x76`  
  `00:00:03.985 I2C: BME280 found at 0x77`  
  `00:00:03.987 I2C: BH1750 found at 0x23`  
  `00:00:03.988 I2C: INA219 found at 0x40`  
  `00:00:03.989 I2C: INA219 found at 0x41`  
  `00:00:03.990 I2C: INA219 found at 0x44`      
- also using the `i2cscan` command you can see the detected I²C devices.   
  `21:11:38.107 CMD: i2cscan`  
  `21:11:38.129 MQT: stat/Sonoff_Baro_1/RESULT = {"I2CScan":"Device(s) found at 0x23 0x40 0x41 0x44 0x76 0x77"}`     
- you can also enable and disable I2C devices using the `I2cDriver` command (they are always enabled by default). More details ([here](https://tasmota.github.io/docs/I2CDevices/#look-at-pre-compiled-builds-to-see-which-driver-is-compiled-in-the-release-binarys)).  
  `21:12:52.527 CMD: I2cDriver`  
  `21:12:52.534 MQT: stat/Sonoff_Baro_1/RESULT = {"I2CDriver":"3,4,5,7,10,11,14,47"}`  
  `21:13:45.850 CMD: I2cDriver14 0`  
  `21:13:45.857 MQT: stat/Sonoff_Baro_1/RESULT = {"I2CDriver":"3,4,5,7,10,11,!14,47"}`   

## 1. 
**Reserved I²C addresses:**  
- 0x00 - Reserved - General Call Address.  
- 0x01 - Reserved for CBUS Compatibility.  
- 0x02 - Reserved for I²C-compatible Bus Variants.  
- 0x03 - Reserved for Future Use.  
- 0x04, 0x05, 0x06, 0x07 - Reserved for Hs-mode Master.  
- 0x78, 0x79, 0x7A, 0x7B - Reserved for 10-bit I²C Addressing.  
- 0x7C, 0x7D, 0x7E, 0x7F - Reserved for Future Purposes.  

## 2. 
**If it is necessary to "increase the capacity" of the I²C bus, then it is necessary to use - the PCA9515A repeater:**
- no software support required (!).   
https://aliexpress.ru/item/32757561351.html   
https://www.ti.com/lit...pdf?&ts=1589295453250   
https://www.onsemi.com...lateral/PCA9517A-D.PDF  

![1.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20bus/I2C%201.1%20.jpg) 

## 3. 
**If it is necessary to bypass the same addresses on the I²C bus, then it is necessary to use - TCA9548A multiplexer:**
- software support required (!!!), now (02/01/2021) is not supported in Tasmota.   
https://aliexpress.ru/item/4000067621113.html   
https://www.ti.com/lit/ds/symlink/tca9548a.pdf 

![2.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20bus/I2C%202.1%20.jpg)
![3.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20bus/I2C%203.1%20.jpg)  

## 4. 
**If it is necessary to logically match the levels (for example 5V and 3.3V), then it is necessary to use - Level Translator PCA9306:**
- [About logic level](https://learn.sparkfun.com/tutorials/logic-levels)   

- no software support required (!).   
https://www.ti.com/lit/gpn/PCA9306  
https://www.sparkfun.com/products/15439  
https://aliexpress.ru/item/4000507058874.html  
https://aliexpress.ru/item/32805554320.html  

## 5. 
**If you need to connect several sensors, you must use - I²C extender:**
- no software support required (!).  
https://aliexpress.ru/item/4001116856790.html   
https://aliexpress.ru/item/1005001351911782.html   
https://aliexpress.ru/item/32964147782.html   
https://aliexpress.ru/item/32965171426.html   
https://www.ebay.com/itm/I2C-IIC-Extender-for-Arduino-Sensor-Shield-with-Cable/121200480686     

## 6. 
**It is possible to combine different options (1+2+3+4).**  

## 7. 

**#UPD 1.**   
Manufacturer claims up to 100 feet (~ 30 meters) for each PCA9615 controller:   
https://learn.sparkfun.com/tutorials/qwiic-differential-i2c-bus-extender-pca9615-hookup-guide   
Sell here:
https://aliexpress.ru/item/33018940484.html

**#UPD 2.**    
Here it is generally stated "up to 300 meters" on a twisted pair:   
https://www.ebay.com/itm/RJ45-Differential-I2C-Long-Cable-Extender-PCA9600-with-Boost-Converter-Arduino/121765222831    
https://www.ebay.com/itm/Differential-I2C-Long-Cable-Extender-PCA9600-with-Boost-Converter-for-Arduino/112580556568     

**#UPD 3.**   
The manufacturer claims up to 20 meters if you use two P82B715 controllers:   
https://www.ebay.com/itm/I2C-IIC-Active-Long-Cable-Extender-P82B715-Module-for-Arduino-and-Other-MCUs/112292264539   

**Best regards   
TrDA**
