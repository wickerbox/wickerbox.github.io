---
layout: hardware
title: Temperature Monitor Teensy Hat
description: 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/teensytempmon.png
permalink: 
publish: yes
---

Simple monitor hat with an LCD screen that displays current temperature as sensed by K-type thermocouple through the MAX31855 junction-compensated sensor chip. The board also buzzes at certain preset temperatures. 

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-WNX4SvV/0/O/tempmon-closeup.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-SpSvJJg/0/O/tempmon-oshpreview.png">

The [Github repository](https://github.com/wickerbox/Teensy-Hats/tree/master/Temperature-Monitor-Hat) has the [manufacturing files](https://github.com/wickerbox/Teensy-Hats/blob/master/Temperature-Monitor-Hat/hardware/gerbers/temperature-monitor-hat-v1.0-gerbers.zip?raw=true) and the [Teensy sketch](https://raw.githubusercontent.com/wickerbox/Teensy-Hats/master/Temperature-Monitor-Hat/software/TeensyMAX31855ReflowOven/TeensyMAX31855ReflowOven.ino). The project is released as open hardware under the CERN v1.2 Open Hardware license. 

I've <a href="https://oshpark.com/shared_projects/PHf0oqic">shared the project at OSH Park</a> so you can buy a set of three bare boards for $22.55, or $7.51 per board.  

The Teensy 3.2 is available at <a href="http://pjrc.com/teensy/index.html">PJRC.com</a> or at OSH Park as an add-on at checkout. I'm using a standard <a href="https://www.adafruit.com/product/181">16x2 LCD screen from Adafruit</a>.

The rest of the parts are available at [Digikey](http://digikey.com). If this is your first time building a board, check out our [assembly howto](/kicad-workflow/assembly/) and remember to always buy a few extra of the capacitors and resistors. They're very small, easy to lose, and often cost 30 cents for three but a dollar for 100.


|Ref|Qty|Description|Maker|Part Number|
|---|---|-----------|------------|------|
|U1|1|IC CONV THERMOCOUPLE MAX31855 SOIC8|Freescale NXP|MAX31855KASA+|
|C1,C2|2|CAP CER 0.1UF 100V X7R 0603|Murata|GRM188R72A104KA35D|
|J2|1|CONN TERM SCREW GREEN 2.54MM 2POS TH|OnShoreTech|OSTVN02A150|
|R1|1|TRIMMER 10K OHM TH|Bourns|3362U-1-103LF|
|SPK1|1|BUZZER ONE NOTE 3V 4KHZ PIEZO SMT|CUI Inc|CMT-1603-SMT-TR|

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-9nPxDFq/0/O/tempmon-inuse.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-TnPWGpb/0/O/tempmon-sideview.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-ZnjP27n/0/O/tempmon-backview.png">

<img src="https://photos.smugmug.com/Projects/Teensy-Hats/i-KG6hJkt/0/XL/tempmon-schematic-XL.png">


