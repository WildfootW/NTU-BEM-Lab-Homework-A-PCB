# NTU-BEM-Lab Homework-A PCB

## Todoist
* [x] Replace Power Connector
* [x] Replace all SMT to 0603
* [x] Digital Vcc Decoupling Capacitor
* [x] Buck Converter ~~LM2576~~ LM2596
* [x] Analog Avcc Decoupling Capacitor
* [x] Light Sensor
* [x] Add PhotoCell
* [ ] Add Border on PCB
* [ ] Change DHT22 to Header
* [ ] Add Screw Hole

## Componenet
* ATmega328P
    * [Datasheet](http://ww1.microchip.com/downloads/en/DeviceDoc/ATmega48A-PA-88A-PA-168A-PA-328-P-DS-DS40002061B.pdf)
    * AD Library from Manufacturer Part Search

* XBee
    * [Datasheet](https://www.sparkfun.com/datasheets/Wireless/Zigbee/XBee-Datasheet.pdf)
    * AD Library from SnapEDA

* DS18B20
    * [Datasheet](https://datasheets.maximintegrated.com/en/ds/DS18B20.pdf)
    * AD Library from Manufacturer Part Search
    * [1-Wire Hub](http://pvlng.com/1-Wire_Hub)

* DHT22
    * [Datasheet](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)
    * [AD Library from SnapEDA](https://www.snapeda.com/parts/DHT22/Aosong%20Electronics/view-part/?ref=search&amp;t=DHT22&amp;company=&amp;welcome=home)

* [Common Light Sensors](https://www.intorobotics.com/common-budgeted-arduino-light-sensors/)
    * ~~VT90N1 (Light Dependent Resistor)~~
        * [Datasheet](https://datasheet.ciiva.com/1249/919043-1249344.pdf?src-supplier=Element14)
        * AD Library from Manufacturer Part Search
    * ~~TSL235R~~
        * [Datasheet](https://datasheet.ciiva.com/1176/323585-1176657.pdf?src-supplier=Newark)
        * AD Library from Manufacturer Part Search
    * PDV-P8103
        * [Datasheet](https://media.digikey.com/pdf/Data%20Sheets/Photonic%20Detetectors%20Inc%20PDFs/PDV-P8103.pdf)

* Power Supply
    * [AMS1117-3.3 over-heating and blow up way below max current](https://electronics.stackexchange.com/questions/274510/ams1117-3-3-over-heating-and-blow-up-way-below-max-current)
    * ~~LM2576~~
        * [Datasheet](https://datasheet.ciiva.com/6597/lm2576hv-6597211.pdf?src-supplier=Digi-Key)
        * AD Library from Manufacturer Part Search
        * ELECTRICAL CHARACTERISTICS LM2576-3.3 - 6V ≤ VIN ≤ 40V, 0.5A ≤ ILOAD ≤ 3A
    * LM2596
        * [Datasheet](https://www.ti.com/lit/ds/symlink/lm2596.pdf)
    * AMS1117 (LM1117)
        * [Datasheet](http://www.advanced-monolithic.com/pdf/ds1117.pdf)

## Schematic Reference
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
### SMD / SMT
* [Difference between 1206, 0805 and 0603 SMD resistor](https://electronics.stackexchange.com/questions/375637/difference-between-1206-0805-and-0603-smd-resistor)
    * > If you need to hand solder them, I suggest not going too small,e specially if you do not have any experience. 0603 should be fine for almost everyone, 0805 even more so, 1206 is a huge beast you can solder with your hands tied and your eyes closed.
