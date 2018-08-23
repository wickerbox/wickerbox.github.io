---
layout: hardware
title: Atmega328 Breakout v1.2
description: 
type: project
destination: wickerbox-electronics
category: breakout-boards 
subcat: 
location: Oregon
image: /img/thumbs/atmega328.png
permalink: 
publish: yes
---

This is a breakout board for the Atmega328. It supports input voltage up to 16V, regulating down to 5V for the microcontroller. A bootloader can be loaded over ICSP and then the board can be powered and communicated with over an FTDI cable. All the input/output pins are broken out for prototyping.

We've made an open source [AVR programmer](/projects/avr-programmer/) that's handy for putting a bootloader on a brand new board. 

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-NQDSG9j/0/O/i-NQDSG9j.png">

The [Github repository](https://github.com/wickerbox/Basic-Breakout-Boards/tree/master/atmega328) has the [manufacturing files](https://github.com/wickerbox/Basic-Breakout-Boards/blob/master/atmega328/gerbers/atmega328-v1.2-gerbers.zip?raw=true). The project is released as open hardware under the CERN v1.2 Open Hardware license.

I've <a href="https://oshpark.com/shared_projects/Bx0lZ6cN">shared the project at OSH Park</a> so you can buy a set of three bare boards for $13.35, or $4.45 per board.

The parts are available at [Digikey](http://digikey.com). If this is your first time building a board, check out our [assembly howto](/kicad-workflow/assembly/) and remember to always buy a few extra of the capacitors and resistors. They're very small, easy to lose, and often cost 30 cents for three but a dollar for 100.

|Ref|Qty|Description|Digikey PN|
|---|---|-----------|------|
|C2 C6|2|CAP CER 10UF 25V X7R 1210|587-2599-1-ND|
|C3 C4|2|CAP CER 22pF 100V C0G NP0 0603|399-11145-1-ND|
|C7 C8 C9 C1 C5|5|CAP CER 0.1UF 100V X7R 0603|490-3285-1-ND|
|D1|1|TVS DIODE 14VWM 23.2VC SMAJ14A-13-F SMA|SMAJ14A-FDICT-ND|
|D2 D3|2|DIODE SCHOTTKY 20V 1A SMA|SS12-E3/61TGICT-ND|
|F1|1|RESETTABLE FUSE 1.1A 25V MF-MSMF|MF-MSMF110/24X-2CT-ND|
|J1|1|CONN TERM SCREW GREEN 2.54MM 2POS TH|ED10561-ND|
|J2|1|HEADER MALE 6POS TH 1x06 0.1”|952-1902-ND|
|J3|1|HEADER MALE 6POS 2x3 0.1”|952-1921-ND|
|J4 J5|2|HEADER FEMALE 12POS TH 1x12 0.1”|952-1905-ND|
|JP1|1|SHUNT JUMPER 0.1IN BLACK GOLD|3M9580-ND|
|LED1|1|LED AMBER DIFFUSED 0603 SMD|475-2712-1-ND|
|R1|1|RES SMD 10K OHM 5% 1/8W 0805|311-10KARCT-ND|
|R2|1|RES SMD 220 OHM 5% 1/10W 0603|311-22GRCT-ND|
|S1|1|SWITCH TACTILE SPST-NO 0.05A 12V|SW1020CT-ND|
|U1|1|IC REG LDO 5V 1.1A NCP1117 DPAK| NCP1117DT50GOS-ND|
|U2|1|IC MCU 8BIT 32KB FLASH 32TQFP|ATMEGA328P-AU-ND|
|X1|1|CRYSTAL 16MHz 18pF 40 OHM 4SMD|CTX1206CT-ND|

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-msrnz4m/0/O/i-msrnz4m.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-GRrkVqp/0/O/i-GRrkVqp.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-4r6X4mz/0/O/i-4r6X4mz.png">


