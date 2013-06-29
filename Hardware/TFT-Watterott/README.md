# Hardware V3.0

## 23.06.2013: Start with V2 Hardware

### SWD-Connector (SWD_CON)

* added:   Mini-SWD Connector (SWD_CON), 1X4, 2.54mm SMT
* changed: Pin 29 (SWCLK) to SWD_CON-2
* changed: Pad 29 to Pin 22 (P0.6 SCK0)
* changed: Pin 39 (SWDIO) to SWD_CON-3
* changed: Pad 39 to Pin 30 (AD6)
* added:   Pin  3 (Reset) to SWD_CON-4
* added:   GND to SWD_CON-1

![Revision G01](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/MI0283QT_v20.jpg)

## 24.06.2013: Changed ISP and Reset

### ISP

* added:   ISP Pullup 10k

### Reset

* added:   Diode, so Reset high (from CON1 or CON2) does not disturb SWD Reset
* changed: Reset Pullup (R11) from 100k to 22k

![Revision G02](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/Reset_ISP.jpg)

## 26.06.2013: Added Adapter Interrupt

### Busy Interrupt via P0[3]

To show the device that the Adapter is busy, P0[3] is set low. So the device can wait until slow commands like 'Clear' are executed.

Sample (device code):

	//clear blue
	cmd_lcd_clear(COL_BLUE);
	//ms_delay(50); //wait
	busy_wait;

The old 50 ms delay wasn't working. Clearing needs about 110 ms....

###  TP Interrupt via P0[3]
To show the device that the TP has been used, it's generating an interrupt also.
So the device doesn't need to read *CMD_TP_POS*, just wait for an interrupt...


Sample (device code):

	while(1)							//endless loop
	{
	//get position if TP touched
	 if(busy_down)						//if TP interrupt is triggered
	{
	//read touched position
	  cmd_tp_pos();
	...

## 27.06.2013: Decided to change MCU

This nice LPC1317 is a by far better MCU for my needs. Ordered a few today...

![Revision G02](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/MI0283QT_v2G1.jpg)

## 28.06.2013: Preliminary Migration Table

Pin functions are nearly the same, but of course 32bit ports of LPC1317 have different names.
 
Same pin, same function, different name. No changes of hardware are required.

	LPC1114        LPC1317
	==============================
	Name    Pin    Name   Function
	------------------------------
	P0.11   32     P0.11  AD0
	P1.0    33     P0.12  AD1
	P1.1    34     P0.13  AD2
	P1.2    35     P0.14  AD3
	P1.4	40	   P0.16  AD5
	P1.6    46     P0.18  RxD
	P1.7    47     P0.19  TxD
	P1.9    17     P0.21  Timer16B1MAT0
	P1.10   30     P0.22  AD6
	P2.0     2     P1.19  GPIO
	P2.1    13     P1.20  GPIO
	P2.2    26     P1.21  GPIO
	P2.3    38     P1.22  GPIO
	P2.6     1     P1.25  GPIO
	P2.7    11     P1.26  GPIO
	P2.8    12     P1.27  GPIO
	P2.9    24     P1.28  GPIO
	P2.10   25     P1.31  GPIO
	P2.11   31     P1.29  GPIO
	P3.0    36     P1.13  GPIO

Different pin, different name. V2 wiring has to be changed.

	LPC1114        LPC1317
	====================================
	Name    Pin    Name    Pin  Function
	------------------------------------
	P2.4    19     P1.23   18   GPIO
	P2.5    20     P1.24   21   GPIO
	P3.5    21     P0.7    23   GPIO	

## 29.06.2013: The new LPCXpresso2-LPC1317...

...is a nice toy.

![Revision G02](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/LPCXpresso2-1.jpg)

Fast with the new LPC1317 and easy to debug with the new LPC-Link2.

![Revision G02](https://raw.github.com/GSNT/TFT-Stuff/master/Hardware/TFT-Watterott/LPCXpresso2-2.jpg)

