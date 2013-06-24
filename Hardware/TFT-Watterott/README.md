# Hardware V3.0

## 23.06.2013: Start with V2 Hardware

### SWD-Connector

* added:   Mini-SWD Connector, 4-pol 2.54 SMD
* changed: Pin 29 an SWD-CON
* changed: PAD 29 an Pin 22 (P0.6 SCK0)
* changed: Pin 39 an SWD-CON
* changed: PAD 39 an Pin 30 (AD6)

![Revision G01](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/MI0283QT_v20.jpg)

## 24.06.2013: Changed ISP and Reset

### ISP

* added:   ISP Pullup

### Reset

* added:   Diode, so Reset high (from CON1 or CON2) does not disturb SWD Reset
* changed: Reset Pullup from 100k to 22k

	
![Revision G02](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/Reset_ISP.jpg)
