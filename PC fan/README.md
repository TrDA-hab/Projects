# 0. About using 4pin PC fan.

- Using [PWM](https://tasmota.github.io/docs/Commands/#pwm).
- Using [MultiPwm](https://tasmota.github.io/docs/Commands/#setoption68).
- Using [DC18B20](https://tasmota.github.io/docs/DS18x20/).  
- Using [Thermostat](https://tasmota.github.io/docs/Thermostat/).
- About sizes [PC fan](https://digitalworld839.com/computer-case-fan-sizes/).  
- About [PC fan](https://en.wikipedia.org/wiki/Computer_fan) (wikipedia).  
- About [Fan sppd regulators](https://www.maximintegrated.com/en/design/technical-documents/tutorials/1/1784.html).
- [PC Fan datasheet](https://noctua.at/pub/media/wysiwyg/Noctua_PWM_specifications_white_paper.pdf).
- [# 9238](https://github.com/arendst/Tasmota/issues/9238)
- [# 11257](https://github.com/arendst/Tasmota/discussions/11257)  
- An [example](https://www.thingiverse.com/thing:4163250) of the practical use of the 4pin PC fan for home ventilation.   

### 4pin PC fan Wire Diagrams.     
*!!! cable coloring varies from fan to fan*   

Pin|Name|Color-1|Color-2|Color-3|Color-4|  
:-:|:-:|:-:|:-:|:-:|:-:|  
|1|GND|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=GREY&color=lightgrey)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|   
|2|+12VDC|![](https://img.shields.io/static/v1?label=&message=RED&color=red)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=GREY&color=lightgrey)|![](https://img.shields.io/static/v1?label=&message=YELLOW&color=yellow)|   
|3|TACH|![](https://img.shields.io/static/v1?label=&message=YELLOW&color=yellow)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=GREY&color=lightgrey)|![](https://img.shields.io/static/v1?label=&message=GREEN&color=greem)   
|4|PWM|![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|![](https://img.shields.io/static/v1?label=&message=BLACK&color=black)|![](https://img.shields.io/static/v1?label=&message=GREY&color=lightgrey)|![](https://img.shields.io/static/v1?label=&message=BLUE&color=blue)|   

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PC%20fan/500-4.jpg)  


# 1. Minimum configuration:  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PC%20fan/501.jpg)  

# 2. Midle configuration:  

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PC%20fan/502.jpg)  

# 3. Maximum configuration:  

### Note:
Now (09/07/2021) Tasmota has no support for the TAСH (tachometer) sensor. Maybe support for the TAСH will be added at a later date.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PC%20fan/503.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PC%20fan/504.jpg)  

**Best regards,  
TrDA.**
