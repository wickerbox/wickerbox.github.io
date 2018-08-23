---
layout: hardware
title: AVR Programmer Board
description: 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/avrprogrammer.png
permalink: 
publish: yes
---

This is meant as a dedicated board containing Nick Gammon's [Arduino Programmer sketch](http://www.gammon.com.au/bootloader) to flash bootloaders on new boards containing unprogrammed AVR microcontrollers.

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-qhd8qMp/0/O/i-qhd8qMp.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-ChNgRFf/0/O/i-ChNgRFf.png">

**Setting up the Board**

You'll only have to do this once.

Grab a copy of Nick Gammon's [Arduino Programmer sketch](http://www.gammon.com.au/bootloader) and the Arduino IDE. You'll also need an Arduino Uno or other AVR board to program this one.

Follow Nick's instructions to connect the six pins of the 2x3 ISP header to the right pins of the programmer board. 

Flip the switch to TARGET and follow Nick's instructions to put the bootloader on the AVR Programmer.

**Programming Other Boards**

Connect the pins of the 2x3 6-pin ISP header to the target board. 

Flip the onboard switch to PROG.

Connect the board to your computer with an FTDI cable and open the Arduino IDE or a serial terminal. 

Set the baud rate to 117500 and press the reset button on the board. The board will reset and run Nick's bootloader sketch while automatically begin talking to the computer over the serial terminal. The sketch will look for your target board and report whether it was found.

If it was found, follow the instructions to apply the appropriate bootloader. If not, troubleshoot the circuitry on your target board. 

**Bill of Materials**

You can get the documentation PDF, an uploadable Digikey .csv file, and the board manufacturing files in [this zip file](https://github.com/wickerbox/Basic-Breakout-Boards/blob/master/avr-programmer/avr-programmer-v1.1.zip?raw=true). The rest of the files are at the [Github repo](https://github.com/wickerbox/Basic-Breakout-Boards/tree/master/avr-programmer).

I've shared the board files at [OSH Park](https://oshpark.com/shared_projects/WKQhn1aU) and I've shared the [cart at Digikey](http://www.digikey.com/short/3dvn71).

The board costs $5.25 for a set of three, or $1.75 per bare board.

One board of parts costs $8.48, but I recommend rounding up on the caps and resistors at least. They're extremely cheap ($1 for a hundred) and easy to lose if you're assembling by hand.

|Ref|Qty|Description|Digikey PN|
|---|---|-----------|------|
|C2 C3|2|CAP CER 22pF 100V C0G NP0 0603|399-11145-1-ND|
|C4|1|CAP CER 1UF 25V X7R 0603|587-2984-1-ND|
|C5 C6 C1|3|CAP CER 0.1UF 100V X7R 0603|490-3285-1-ND|
|J1|1|HEADER MALE 6POS TH 1x06 0.1”|952-1902-ND|
|J2|1|HEADER MALE 6POS 2x3 0.1”|952-1921-ND|
|R1|1|RES SMD 10K OHM 5% 1/8W 0805|311-10KARCT-ND|
|S1|1|SWITCH TACTILE SPST-NO 0.05A 12V|SW1020CT-ND|
|S2|1|SWITCH SLIDE SPDT 200MA 30V|EG1903-ND|
|U1|1|IC MCU 8BIT 32KB FLASH 32TQFP|ATMEGA328P-AU-ND|
|X1|1|CRYSTAL 16MHz 18pF 40 OHM 4SMD|CTX1206CT-ND|

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-KSQZQKD/0/O/i-KSQZQKD.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-HjHgss8/0/O/i-HjHgss8.png">


