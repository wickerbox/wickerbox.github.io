---
layout: hardware
title: LCD-LiDAR-SD Teensy Hat
description: 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/teensylcdlidarsd.png
permalink: 
publish: yes
---

Print out LiDAR distances values on an LCD screen and save them to a microSD card. This board is based on the <a href="https://github.com/pulsedlight3d">LiDAR-Lite v1 and v2</a>.

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-g3pkCsc/0/O/lcdlidarsd-frontview.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-sn5RSdz/0/O/lcdlidarsd-oshpreview.png">

The [Github repository](https://github.com/wickerbox/Teensy-Hats/tree/master/LCD-LiDAR-SD-Hat) has the [manufacturing files](https://github.com/wickerbox/Teensy-Hats/blob/master/LCD-LiDAR-SD-Hat/gerbers/teensy-lcd-lidar-sd-hat-v1.0-gerbers.zip?raw=true) and the [Teensy sketch](https://raw.githubusercontent.com/wickerbox/Teensy-Hats/master/LCD-LiDAR-SD-Hat/software/Teensy-LCD-LiDAR-SD-Hat/Teensy-LCD-LiDAR-SD-Hat.ino). The project is released as open hardware under the CERN v1.2 Open Hardware license.

I've <a href="https://oshpark.com/shared_projects/BkOPlbFA">shared the project at OSH Park</a> so you can buy a set of three bare boards for $22.55, or $7.51 per board. 

The Teensy 3.2 is available at <a href="http://pjrc.com/teensy/index.html">PJRC.com</a> or at OSH Park as an add-on at checkout. I'm using a standard <a href="https://www.adafruit.com/product/181">16x2 LCD screen from Adafruit</a>.

The rest of the parts are available at [Digikey](http://digikey.com). If this is your first time building a board, check out our [assembly howto](/kicad-workflow/assembly/) and remember to always buy a few extra of the capacitors and resistors. They're very small, easy to lose, and often cost 30 cents for three but a dollar for 100.

|Ref|Qty|Description|Manuf|Mfr PN|Source PN|
|---|---|-----------|-----|------|---------|
|J2|1|HEADER FEMALE 6POS TH 1x06 0.1”|Harwin|M20-7820642|952-1808-ND|
|J3|1|CONN MICRO SD CARD |Molex|0475710001|WM9731CT-ND|
|LED1-2|2|LED AMBER DIFFUSED 0603 SMD|OSRAM Opto|LA L296-Q2R2-1-Z|475-2712-1-ND|
|R1-R5,R7|6|RES SMD 1K OHM 1% 1/10W 0603|Samsung|RC1608F102CS|1276-3484-1-ND|
|R6|1|TRIMMER 10K OHM TH |Bourns| 3362U-1-103LF|3362U-103LF-ND|
|S1-S3|3|SWITCH TACTILE SPST-NO 0.05A 12V|Omron|B3U-1000P|SW1020CT-ND|

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-bc4Fc9r/0/O/lcdlidarsd-backview.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-nRtWMd8/0/O/lcdlidarsd-sideview.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-ZnjP27n/0/O/tempmon-backview.png">

