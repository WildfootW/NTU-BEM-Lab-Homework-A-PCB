# NTU-BEM-Lab Homework-A PCB

## Todoist
* [x] Replace Power Connector
* [x] Replace all SMT to 0603
* [x] Digital Vcc Decoupling Capacitor
* [x] Buck Converter ~~LM2576~~ ~~LM2596~~ LM1117
* [x] Analog Avcc Decoupling Capacitor
* [x] Light Sensor
* [x] Add PhotoCell
* [x] Add Border on PCB
* [x] Change DHT22 to Header
* [x] Add Screw Hole

## Componenet
* ATmega328P
    * [Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/ATmega48A-PA-88A-PA-168A-PA-328-P-DS-DS40002061B.pdf)

* XBee
    * [Datasheet](https://www.sparkfun.com/datasheets/Wireless/Zigbee/XBee-Datasheet.pdf)

* DS18B20
    * [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)
    * [1-Wire Hub](http://pvlng.com/1-Wire_Hub)

* DHT22
    * [Datasheet](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)

* [Common Light Sensors](https://www.intorobotics.com/common-budgeted-arduino-light-sensors/)
    * ~~VT90N1 (Light Dependent Resistor)~~
        * [Datasheet](https://datasheet.ciiva.com/1249/919043-1249344.pdf?src-supplier=Element14)
    * ~~TSL235R~~
        * [Datasheet](https://datasheet.ciiva.com/1176/323585-1176657.pdf?src-supplier=Newark)
    * PDV-P8103
        * [Datasheet](https://media.digikey.com/pdf/Data%20Sheets/Photonic%20Detetectors%20Inc%20PDFs/PDV-P8103.pdf)

* Power Supply
    * [AMS1117-3.3 over-heating and blow up way below max current](https://electronics.stackexchange.com/questions/274510/ams1117-3-3-over-heating-and-blow-up-way-below-max-current)
    * [5V Voltage Regulator, LM7805 vs LM2940 vs LM1117 vs AMS1117](https://jpralves.net/post/2015/05/19/5v-voltage-regulator.html)
    * ~~LM2576~~
        * [Datasheet](https://datasheet.ciiva.com/6597/lm2576hv-6597211.pdf?src-supplier=Digi-Key)
        * ELECTRICAL CHARACTERISTICS LM2576-3.3 - 6V ≤ VIN ≤ 40V, 0.5A ≤ ILOAD ≤ 3A
    * ~~LM2596~~
        * [Datasheet](https://www.ti.com/lit/ds/symlink/lm2596.pdf)
        * Diode is too big ([1N5820](https://www.mouser.tw/ProductDetail/ON-Semiconductor/1N5820G?qs=y2kkmE52mdMaZomtu%252BD%252BfQ%3D%3D)) (Can use 2N4001 instead of)
        * Overkill
        * 4.75 V ≤ VIN ≤ 40 V, 0.2 A ≤ ILOAD ≤ 3 A
        * ![](https://i.imgur.com/l2wso2I.png)
    * ~~AMS1117~~
        * [Datasheet](http://www.advanced-monolithic.com/pdf/ds1117.pdf)
        * Out of Stock
    * LM1117
        * [Datasheet](https://www.ti.com/lit/ds/symlink/lm1117.pdf?HQS=TI-null-null-mousermode-df-pf-null-wwe&DCM=yes&ref_url=https%3A%2F%2Fwww.mouser.tw%2F&distId=26)

# Reference
## Libraries
* [Celestial Altium Library](https://altiumlibrary.com/)
* [SamacSys](https://www.samacsys.com/altium-designer-library-instructions/)

## Component Considerations
### ATmega328P
* [Electrical Engineering - What is the minimal set of parts for a circut with this AVR microcontroller?](https://electronics.stackexchange.com/questions/53713/what-is-the-minimal-set-of-parts-for-a-circut-with-this-avr-microcontroller)
* [AVR® Microcontroller Hardware Design Considerations](https://www.microchip.com/wwwAppNotes/AppNotes.aspx?appnote=en591472)
    * 2.1 Ditital Supply
        * Put decoupling capacitors near IC
        * For devices with multiple pairs of power and ground pins, it is essential that there is a decoupling capacitor for every pair of pins.
    * 2.2 Analog Supply
        * Avcc ensures the analog circuits are less prone to the digital noise
        * AREF must also be decoupled. The typical value is 100 nF
        * If a separate AGND is present, the ground should be separated from digital ground. (analog & digital grounds are connected only at power supply GND)
    * 3 Connection of RESET Pin on AVR Devices
        * The recommended pull-up resistor value is 4.7 kΩ (For DebugWIRE to function properly, the pull-up must not be less than 10 kΩ)
        * Using an extra capacitor is an additional protection. (cannot be used when DebugWIRE or PDI is used)
        * Recommend add an ESD protection diode (cannot work with HVPP). Alternatively, a Zener diode can be used to limit the Reset voltage relative to GND (highly recommended in noisy environments).
    * 3.1 External RESET Switch
        * It is important to add a series resistance (330R)
    * 4.1 SPI Programming Interface
        * A few ISP programmers are powered by the target power supply. In this way they easily adapt to the correct voltage level of the target board.
        * Other ISP programmers, such as STK600, can alternatively power the target board via the VTG line. In such a case, it is important that the power supply on the target is not switched on.

* Crystal Oscaillator 16MHz
    * Table 8.3 - 12-22 pF
* debugWIRE
* Serial Interface

## Others Considerations
### SMD / SMT
* [Difference between 1206, 0805 and 0603 SMD resistor](https://electronics.stackexchange.com/questions/375637/difference-between-1206-0805-and-0603-smd-resistor)
    * > If you need to hand solder them, I suggest not going too small,e specially if you do not have any experience. 0603 should be fine for almost everyone, 0805 even more so, 1206 is a huge beast you can solder with your hands tied and your eyes closed.
* 0603(0.06 inch * 0.03 inch) == 1603 (1.6 mm * 0.8 mm)
### Trace Rules
* [PICKING THE RIGHT TRACE WIDTH FOR YOUR NEXT PCB DESIGN](https://bayareacircuits.com/picking-the-right-trace-width-for-your-next-pcb-design/#:~:text=While%200.003%E2%80%9D%20can%20be%20a,voltage%20traces%20should%20be%20larger.)

