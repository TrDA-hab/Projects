## About I2C bus:
- [Wikipedia](https://en.wikipedia.org/wiki/I%C2%B2C)  
- [Sparkfun](https://learn.sparkfun.com/tutorials/i2c)  
- [Supported I2C devices](https://tasmota.github.io/docs/I2CDevices/#supported-i2c-devices)  

## 0. 
**About using the I2C bus:**
- the maximum allowable bus capacitance is 400 pF, the bus length does NOT matter.
- it is not allowed to use devices with the same addresses.
- the maximum number of devices on the I2C bus is no more than 126 pcs. Addresses from 0 to 125, one for "master" and others for "slave".
- ready-made I2C modules, already have pull-up resistors, and you should not worry.
- if you need a "longer" I2C bus, you must use a repeater ([1](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#1)).  
- if you need more devices with the same address, you must use a multiplexer ([2](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#2)).  
- if it is necessary to logically match the levels, you must use alevel translator ([3](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#3)).
- if you need to connect several sensors, you must use I2C extender ([4](https://github.com/TrDA-hab/Projects/blob/master/I2C%20bus/README.md#4)).
- I2C bus allows connecting hot-swappable (hot) modules.
- for the I2C bus, you can use the Rx and Tx of your ESP8266.

## 1. 
**If it is necessary to "increase the capacity" of the I2C bus, then it is necessary to use - the PCA9515A repeater:**

![1.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20bus/I2C%201.1%20.jpg)
- no software support required (!).   
https://aliexpress.ru/item/32757561351.html   
https://www.ti.com/lit...pdf?&ts=1589295453250   
https://www.onsemi.com...lateral/PCA9517A-D.PDF   

## 2. 
**If it is necessary to bypass the same addresses on the I2C bus, then it is necessary to use - TCA9548A multiplexer:**
![2.1](https://raw.githubusercontent.com/TrDA-hab/Projects/master/I2C%20bus/I2C%202.1%20.jpg)
- software support required (!!!), now (02/01/2021) is not supported in Tasmota.   
https://aliexpress.ru/item/4000067621113.html   
https://www.ti.com/lit/ds/symlink/tca9548a.pdf   

## 3. 
**If it is necessary to logically match the levels (for example 5V and 3.3V), then it is necessary to use - Level Translator PCA9306:**
- [About logic level](https://learn.sparkfun.com/tutorials/logic-levels)   

- no software support required (!).   
https://www.ti.com/lit/gpn/PCA9306  
https://www.sparkfun.com/products/15439  
https://aliexpress.ru/item/4000507058874.html  
https://aliexpress.ru/item/32805554320.html  

## 4. 
**If you need to connect several sensors, you must use - I2C extender:**
- no software support required (!).  
https://aliexpress.ru/item/4001116856790.html   
https://aliexpress.ru/item/1005001351911782.html   
https://aliexpress.ru/item/32964147782.html   
https://aliexpress.ru/item/32965171426.html   
https://www.ebay.com/itm/I2C-IIC-Extender-for-Arduino-Sensor-Shield-with-Cable/121200480686     

## 5. 
**It is possible to combine different options (1+2+3+4).**  

...

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
