# EMS bus info page

## EMS bus interface schematic
If you only intend to read out the bus, you just need to build the top part of the schematic (the RX part), and the 100nF capacitor from the bottom part.
When you also want to write to the bus build the entire schematic.
![EMS bus interface schematic](http://www.mikrocontroller.net/attachment/95287/EMS_Interface.png)

(The schematic is originally from the website http://wiki.neo-soft.org and it is the reverse engineered schematic of a Buderus service key).

Depending on which Arduino you use connect the RX pin of the Arduino serial port to the RX_OUT pin in the schematic.
TX goes to TX_IN. Do not connect the 12V pin of the service jack.
It does not matter which EMS bus pin you connect to which pin, the bridge rectifier will make sure both orientations will work.<br>

The 100nF (=0,1uF) capacitor is a bypass capacitor to ensure a stable voltage for the LM393 (See the LM393 datasheet). 
Also do not forget to power the LM393 itself with 5V for Arduino or 3V3 for ESP and Raspberry. Connect ground on pins 8 and 4.<br>
<br>

The 2 'N/A' components on the left are 2 poly fuses. Include them or not, your choice. A tripping value of about 300mA or so seems like a good value.<br>
The 4 parallel resistors in the transmitter part can be replaced by a single 1W ~250 Ohm resistor. Keep the final resistor value between 210 and 250 Ohm, as this is important for a stable TX.

There are more components that are not that strict, I used f.i. a LM339 instead of the LM393 on my breadboard.
In the schematic there are two BAT54S diodes but you can just use BAT46 for all. You can likely even pull off using 1N4148 everywhere.

Furthermore the 4,7mH inductors are pretty huge, likely 4,7uH is the correct value (I used the latter value in my final designs).<br> Probably someone got the multiplier wrong when decoding the value.

One improvement to the circuit would be using optocouplers on the right side where you interface them with your logic.
Without those in theory a voltage burst on the bus could destroy your Arduino or vice versa.

The line 'U_REF' is an internal voltage for the comparators, just connect every 'U_REF' line together and you are done.

Here is the Rx part of the schematic on a small breadboard (working example, no layout available):

![EMS schematic on a breadboard](https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/master/Documentation/ems-breadboard.JPG?raw=true)

### Using this circuit for interfacing with a Raspberry Pi
You can use this circuit also to directly interface with the Raspberry Pi UART. Just power the circuit with 3V3 instead of 5V.

## Complete interface board
I also created a complete interface board with 5V and 3.3V compatible UART interface. For the design see the [PCB-files](https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/tree/master/PCB-files/V0.9) folder.
You can order a complete and tested board [HERE](https://shop.hotgoodies.nl/ems/).<br>
![EMS bus PCB](https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/master/Documentation/nefit-ems-bus-interface-PCB.jpg)

## EMS bus interface locations
The EMS bus is usually available at two locations; at the front and/or inside the boiler.

### Front service jack
On most boilers there is a 3,5mm service jack at the front of the boiler.

![EMS service jack pinout](https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/master/Documentation/EMS-bus-jack-pinout.JPG?raw=true)

### EMS Thermostat clamps
Aside from the front service jack, you can also connect the 2 EMS bus wires to the thermostat clamps on the inside interface of the boiler. You can connect these in parallel to a EMS thermostat on the same terminal if needed. The EMS bus is a shared bus that allows for multiple devices on the same bus. If needed, you can also put it in parallel where the thermostat is mounted on the wall. 

![EMS thermostat clamps](https://github.com/bbqkees/Nefit-Buderus-EMS-bus-Arduino-Domoticz/blob/master/Documentation/ems-bus-on-boiler.JPG)

You can also use the on/off terminal for an on/off thermostat while simultaneously using the EMS bus terminal for the interface board. So if you have an on/off thermostat you can still communicate with the EMS bus. In fact I use this very setup at home.
