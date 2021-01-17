# DC motor & magnetic Encoder.
### Note:
Now (01/15/2021) Tasmota has no support for "Magnetic Encoder". Perhaps this support will be added later.

## 1. TB6612FNG Motor Driver.
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor2/911.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor2/912.jpg)

## 2. Wemos motor shield V1.
### Note:
Now (01/15/2021) Tasmota has no support for "Wemos motor shield V2". Perhaps this support will be added later.

![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor2/913.jpg)
![](https://raw.githubusercontent.com/TrDA-hab/Projects/master/DC_motor2/914.jpg)

### Rules:

Rule1 
ON Power1#state=1 DO Backlog Counter2 0; driver44 SETMOTOR, 0, 1 ENDON
ON counter#c1>3800 DO Backlog driver44 SETMOTOR, 0, 3; delay 20; Counter1 0; Power1 0 ENDON

Rule2 
ON Power2#state=1 DO Backlog Counter2 0; driver44 SETMOTOR, 0, 2 ENDON
ON counter#c1>3800 DO Backlog driver44 SETMOTOR, 0, 3; delay 20; Counter1 0; Power2 0 ENDON
