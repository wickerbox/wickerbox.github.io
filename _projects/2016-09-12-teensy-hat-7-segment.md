---
layout: hardware
title: Quad 7-Segment Display Teensy Hat
description: 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/teensy7segment.png
permalink: 
publish: yes
---

7-Segment display daughter board for the Teensy 3.2 with an additional SD card connector for reading from. The included code adapts the SevSeg library for the pins used here. 

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-2jq96wZ/0/O/7segment-assembled.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-spfc5bm/0/O/7segment-counting.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-VTZKvz5/0/O/7segment-oshpreview.png">

The [Github repository](https://github.com/wickerbox/Teensy-Hats/tree/master/7-Segment-Hat) has the [manufacturing files](https://github.com/wickerbox/Teensy-Hats/blob/master/7-Segment-Hat/hardware/gerbers/7-segment-display-teensy-hat-v1.1-gerbers.zip?raw=true) and the [Teensy sketch](https://raw.githubusercontent.com/wickerbox/Teensy-Hats/master/7-Segment-Hat/software/Teensy-7Segment/Teensy-7Segment.ino). The project is released as open hardware under the CERN v1.2 Open Hardware license.

I've <a href="https://oshpark.com/shared_projects/spIDCqwD">shared the project at OSH Park</a> so you can buy a set of three bare boards for $5.20, or $1.74 per board.

The Teensy 3.2 is available at <a href="http://pjrc.com/teensy/index.html">PJRC.com</a> or at OSH Park as an add-on at checkout. I'm using a standard <a href="https://www.adafruit.com/product/181">16x2 LCD screen from Adafruit</a>.

The rest of the parts are available at [Digikey](http://digikey.com). If this is your first time building a board, check out our [assembly howto](/kicad-workflow/assembly/) and remember to always buy a few extra of the resistors. They're very small, easy to lose, and often cost 30 cents for three but a dollar for 100.

|Ref|Qty|Description|MF_Name|MF_PN|Digikey|
|---|---|-----------|-------|-----|-------|
|J3|1|CONN MICRO SD CARD HINGED TYPE|Molex|5009010801|WM19081CT-ND|
|LED1|1|LED DISPLAY 4CHAR 7SEGMENT COMMON CATHODE LTC-4727JR|LITE-ON|LTC-4727JR|160-1551-5-ND|
|R1-R4|4|RES SMD 470 OHM 5% 1/4W 0603|Rohm Semi|ESR03EZPJ471|RHM470DCT-ND|

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-PzS9NFN/0/XL/7segment-schematic-XL.png">
