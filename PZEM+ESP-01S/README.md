## Using PZEM-004 (Energy Monitoring)

## ![](https://img.shields.io/static/v1?label=&message=Danger High Voltage!&color=red).
Check if you have disconnected the high voltage.

### More information:
 - [Tasmota PZEM-004](https://tasmota.github.io/docs/PZEM-0XX/)
 - [github-Tasmota PZEM-004 (3 phase)](https://github.com/arendst/Tasmota/issues/2315)
 - [About PZEM-004 (V3)](https://innovatorsguru.com/pzem-004t-v3/)
 - [Modifying PZEM-004T (V3)](https://youtu.be/qRsjsenvlJA)
 - [Schematics PZEM-004 (V3)](https://github.com/TheHWcave/Peacefair-PZEM-004T-/blob/main/PZEM004T-orig.pdf)
 - [Datasheet PZEM-004 (V3)](https://innovatorsguru.com/wp-content/uploads/2019/06/PZEM-004T-V3.0-Datasheet-User-Manual.pdf)
 - [Datasheet V9881D](http://www.vangotech.com/int/uploadpic/152782258251.pdf)
 - [Datasheet CT817C](https://datasheet.lcsc.com/lcsc/1810010617_CT-Micro-International-CT817C-S-T3-H_C191931.pdf)
 
### Cool projects:
 - [x3 phase PZEM-004 V3 (EN)](https://zorruno.com/w/EnergyMonitoringPZEM004T)
 - [x3 phase PZEM-004 V3 (DE)](https://forum.iobroker.net/topic/28453/tutorial-pzem-004t-3-phasen-%C3%BCberwachung)
 - [x3 phase PZEM-004 V3 (PT)](https://forum.cpha.pt/t/como-construir-um-contador-de-energia-de-3-canais/7578)  
 - [x3 phase PZEM-004 V3 (EN)](https://github.com/apreb/eNode)
 - [x3 phase PZEM-004 V3 (EN)](https://www.hackster.io/swisscore/home-power-monitoring-a78c0c)

## Modification PZEM-004 (V3).  
It is necessary to modify PZEM-004 (V3) for correct operation, it is necessary to replace two resistors on each device (**R12** and **R14**).  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-mod0.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-mod1.jpg)  
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-mod2.jpg)  

## PIN configuration

For PZEM-004 (V1/V2):

 Wemos Pin|GPIO|Component|PZEM-004 Signal
:-:|:-:|:-:|:-:
Tx|1|PZEM0XX Tx|Rx
Rx|3|PZEM0XX Rx|Tx

For PZEM-004 (V3):

 Wemos Pin|GPIO|Component|PZEM-004 Signal
:-:|:-:|:-:|:-:
Tx|1|PZEM0XX Tx|Rx
Rx|3|PZEM016 Rx|Tx

 ## How to use it (optional):
1. Run commands in the console to reset values:
 - `EnergyReset1 0`   // reset values for Today  
 - `EnergyReset2 0`   // reset values for Yesterday  
 - `EnergyReset3 0`   // reset values for Total  
2. Run commands in the console to set values:
 - `EnergyReset3 33557123`   // set values for Total (33557123 = 33557.123kWh)
3. Run the commands in the console to set the settings of the two tariff counters "day / night":
 - `tariff1 07:00,23:00`   // set values for tariff 1 (from 07:00 to 23:00)
 - `tariff2 23:00,07:00`   // set values for tariff 2 (from 23:00 to 07:00)

 ## PZEM-004 portable power monitoring unit (x1 phases)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-831.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/graph-0.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-BOX%20v24.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-BOX%20v24-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200829_215858.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200829_220257.jpg)

 ## PZEM-004 DIN rail mounted power monitoring unit x1 phases
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-841.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/graph-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-V4%20v14-2.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-V4%20v14-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200722_221525.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200828_140301.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200828_145518.jpg)

 ## PZEM-004 x3 phase DIN rail mounted power monitoring unit
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM-x3-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/x3_PZEM_v1-2.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/x3_PZEM_v1-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200904_190301.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200904_190441.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200828_181256.jpg)

 ## PZEM-004 PCB boad x3 phases
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/Schematic_ESP-01s%20board%20to%20PZEM-004_2021-03-25.png)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200716_170628.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-2.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-3.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-V3%20v11.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/PZEM004-V3%20v28-1.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200814_165053.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200814_155649.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200828_141101.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/PZEM%2BESP-01S/20200823_180740.jpg)  


## My PCB for x3 phases (open source hardware). For non-commercial use only!:  
 - [easyeda_source](https://github.com/TrDA-hab/Projects/tree/master/PZEM%2BESP-01S/easyeda_source)
 - [gerber files](https://github.com/TrDA-hab/Projects/tree/master/PZEM%2BESP-01S/gerber)

## Another PCB for x1 phase (open source hardware). For non-commercial use only!:
 - [PCB board for PZEM-004 (1 phase)](https://easyeda.com/r.blaszczak/pzem-004t-supla)

#### Additional information (optional!). These are my 3D models for PZEM-004 and BOM. For non-commercial use only!:
 - [PZEM-004 portable power monitoring unit](https://www.thingiverse.com/thing:4583058)
 - [PZEM-004 DIN rail mounted power monitoring unit](https://www.thingiverse.com/thing:4583701)
 - [x3 phase PZEM-004 DIN rail mounted power monitoring unit](https://www.thingiverse.com/thing:4587966)

**Best regards  
TrDA**
