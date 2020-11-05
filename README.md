# NTU-BIME-INSECT-Lab-PCB-Homework

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
* DHT22
    * [Datasheet](https://www.sparkfun.com/datasheets/Sensors/Temperature/DHT22.pdf)
    * [AD Library from SnapEDA](https://www.snapeda.com/parts/DHT22/Aosong%20Electronics/view-part/?ref=search&amp;t=DHT22&amp;company=&amp;welcome=home)
* [Common Light Sensors](https://www.intorobotics.com/common-budgeted-arduino-light-sensors/)
* ~~VT90N1 (Light Dependent Resistor)~~
    * [Datasheet](https://datasheet.ciiva.com/1249/919043-1249344.pdf?src-supplier=Element14)
    * AD Library from Manufacturer Part Search
* TSL235R
    * [Datasheet](https://datasheet.ciiva.com/1176/323585-1176657.pdf?src-supplier=Newark)
    * AD Library from Manufacturer Part Search

# Schematic
## ATmega328P
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

* Crystal Oscaillator 16MHz
    * Table 8.3 - 12-22 pF
* debugWIRE
* Serial Interface
