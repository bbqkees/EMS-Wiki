This page will over time include more information specific to certain thermostats.
Take the details with a grain of salt please. Not everything is verified yet.


## EMS Thermostats

Bus Type | Model ID | EMS ID | Brand and type | Image
---|---|---|---|---
EMS|76|0x10|Sieger ES73|
EMS|79|0x17|Buderus RC10<br>Nefit Moduline 100|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-moduline-100.JPG" width="150">
EMS|||Nefit Moduline 200|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline200.jpg" width="150">
EMS|77|0x17|Buderus RC20<br>Nefit Moduline 300|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline300-400.jpg" width="150">
EMS|93|0x18|Buderus RC20F|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-moduline-100.JPG" width="150">
EMS|78|0x10|Buderus RC30<br>Nefit Moduline 400|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline300-400.jpg" width="150">
EMS|86|0x10|Buderus RC35|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline300-400.jpg" width="150">
EMS|86|0x10|RC35 (built-in version)|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/built-in-RC35.jpg" width="150">
EMS|202|0x18|Buderus TC100<br>Junkers TC100<br>Nefit Easy|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-easy.jpg" height="150">
EMS|206|0x02|Bosch EasyControl|
EMS|158|0x10|Buderus RC310|
EMS|255|0x18|Bosch CW100|
EMS|171|0x02|Bosch / Nefit EMS to Opentherm converter|
EMS/EMS2|165|0x02|Nefit Moduline 1010|
EMS/EMS2|||Nefit Moduline 1000|
EMS/EMS2|||Nefit Moduline 2000|
EMS/EMS2|||Nefit Moduline 2050|
EMS/EMS2|||Nefit Moduline 3000|

Although the hardware of some thermostats is identical (if you open up a ModuLine 300 or 400 it says 'RC35' on the PCB), the firmware will be different. It appears there are also differences in frametypes. However, as more people are using theses sketches this will be resolved over time.<br>

### RC10 ≈ Moduline 100
This is the simplest EMS thermostat.<br>
Bus ID: 0x17.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-moduline-100.JPG" width="150"><br>

#### RC10 specifics

#### Moduline 100 specifics

(Info from http://domoticz.com/forum/viewtopic.php?f=38&t=14132&start=100#p177153)<br>
Read the current temp setting with the following command:<br>
`0x0B,0x97,0xB0,0x04,0x01,<CRC>,<BREAK>`<br>
Write a new temperature setting (0x29 = 41 = 20,5 degrees) with the following command:<br>
`0x0B,0x17,0xB0,0x04,0x29,<CRC>,<BREAK>`<br>
<br>
Reading the room temperature:<br>
(from http://domoticz.com/forum/viewtopic.php?f=38&t=14132&start=100#p177187)<br>
```
17:00:B1:00:04:26:00:CD:00:00:00:CD

0x04 ??? 
0x26 seems to be equal to the set room temperature
0x00:0xCD Delayed current room temp which then would be 20.5 degrees Celsius. (if it is multiplied by 10)
0x00:0x00 ?????
0x00:0xCD Current room temperature.
```

### RC20 ≈ Moduline 200
This is one of the simplest EMS thermostat.<br>
Bus ID: 0x17.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline200.jpg" width="150"><br>

#### RC20 specifics

#### Moduline 200 specifics
Reading the room temperature:<br>
`0x17,0x91,0x02`<br>

Setting temperature:<br>
Setting the temperature for this thermostat depends on the mode the thermostat is in. It has three modes: 0=low, 1=manual, 2=clock.<br>
If it is in clock mode, you need to override the clock setting with `0x17,0xA8,0x1C`<br>
If it is in manual mode, you need to set the manual temperature with `0x17,0xA8,0x1D`<br>



### RC30 ≈ Moduline 300 ≈ Sieger eSR 73
This is one of the more advanced EMS thermostat.<br>
Bus ID: 0x17 OR 0x10.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline300-400.jpg" width="150"><br>

#### RC30 specifics

#### Moduline 300 specifics
Exact same hardware as the Moduline 400, just different firmware.

### RC35 ≈ Moduline 400
This is the most advanced EMS thermostat in the series.<br>
Bus ID: 0x10.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/moduline300-400.jpg" width="150"><br>

These thermostats work with heating zones. It supports up to 4 individual heating zones. Each one of them has it's own registers for setting and reading the temperature.

#### RC35 specifics
For this thermostat have a look at the wonderful documentation of Danidata at his [blog](https://domoticproject.com/ems-bus-buderus-nefit-boiler/).

#### Moduline 400 specifics
If you open up the Nefit Moduline 400 the PCB clearly says "Buderus" and "RC35". See below. <br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/Thermostats/Moduline-400-PCB1.jpg" width="250"><br>
However, it appears not all registers are the same as for the RC35. At the moment work is being done to figure out the control of the Moduline 400.<br>
On the RC35 PCB you can clearly see the EMS bus interface and the super capacitor for storing energy.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/Thermostats/Moduline-400-PCB2.jpg" width="250"><br>

### Nefit Easy ≈ CT100/TC100
This is the newer WiFi enabled EMS bus thermostat.<br>
Bus ID: 0x18.<br>
<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-easy.jpg" height="150"><br>

It is also known as:<br>
- Nefit Easy (Netherlands)
- Junkers Control CT100 (Belgium)
- Buderus Logamatic TC100 (Belgium)
- E.L.M. Touch (France)
- Worcester Wave (UK)
- Bosch Control CT‑100 (Other)

The datagram containing the current room temperature and setpoint is 0x0A.
However, this datagram appears to be read-only so although you can read the temperature etc, it is not possible to change the setpoint via the EMS bus. For more information see the [Github of Proddy](https://github.com/proddy/EMS-ESP-Boiler/blob/13603d63c65feccd3513d4383df0ac9c1b93f464/src/ems.cpp#L687).


Byte 8 and 9 contain the current room temperature (divide by 100) and byte 10 and 11 contain the current setpoint of the room temperature (divide by 100).


**Non-EMS thermostats**

Buderus type | Nefit type | Image
---|---|---
iRT30|ModuLine 30|<img src="https://raw.githubusercontent.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/master/Documentation/nefit-irt30.jpg" width="150">

If you have an older thermostat looking like the one above, your boiler is **NOT** compatible with the EMS bus.
