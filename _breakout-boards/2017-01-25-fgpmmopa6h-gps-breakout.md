---
layout: hardware
title: FGPMMOPA6H GPS Breakout Board
description: 
type: project
destination: wickerbox-electronics
category: breakout-boards
subcat: 
location: Oregon
image: /img/thumbs/fgpmmopa6h.png
permalink: 
publish: yes
---

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-xfcZ7K6/0/O/i-xfcZ7K6.png">

This board carries a GPS module that talks to a microcontroller or computer over serial (UART, RX/TX). You can use it with 3V or 5V microcontrollers. 

- To use it with a computer:
  - Connect a 5V FTDI cable or other FTDI adapter
  - Orient the FTDI cable with the green wire (RESET) at the GPS NC (pin 1)
- To use it with 5V microcontrollers:
  - Connect 5V and GND for the power
  - Connect microcontroller RX to GPS 3.3V_TX
  - Connect microcontroller TX to GPS 5V_RX
- To use it with 3.3V microcontrollers:
  - Connect 3.3V and GND for the power
  - Connect microcontroller RX to GPS 3.3V\_TX
  - Connect microcontroller TX to GPS 3.3V\_RX

1PPS, RTCM, and the FIX are 3.3V-level signals and may not be interpreted correctly by a 5V system. The RTCM must be enabled by the factory so this signal may not work at all on your chip.

**Testing**

Test the board by wiring it up to an Arduino and using the parsing sketch from the [Adafruit GPS](https://github.com/adafruit/Adafruit_GPS) library.  After a minute or so, the chip reported the following fix:

```
Time: 19:51:23.0
Date: 11/3/2017
Fix: 1 quality: 1
Location: 4518.3549N, 12257.4375W
Location (in degrees, works with Google Maps): 45.3059, -122.9573
Speed (knots): 0.21
Angle: 80.31
Altitude: 161.30
Satellites: 4
$PGTOP,11,2*6E
$GPGGA,195124.000,4518.3552,N,12257.4374,W,1,4,3.10,161.0,M,-19.9,M,,*66
$GPRMC,195124.000,A,4518.3552,N,12257.4374,W,0.15,94.82,110317,,,A*4E
```
**Warning!**

The GPS chips are extremely sensitive to the reflow temperatures and should be prebaked even if your other electronics seem to be fine. The GPS chips will power up and report a 2D Fix, so the Adafruit parsing sketch works great, but we had trouble reliably getting them to make a 3D Fix (needed for speed measurements) unless we hand soldered the chips on after reflowing the rest of the parts. 

**Bill of Materials**

I've shared the board files at [OSH Park](https://oshpark.com/shared_projects/nSnH0hWt) and I've shared the [cart at Digikey](http://www.digikey.com/short/3dvnvj).

The board costs $9.45 for a set of three, or $3.15 per bare board.

One board's worth of parts costs $4.79, but I recommend rounding up on the caps and resistors at least. They're extremely cheap ($1 for a hundred) and easy to lose if you're assembling by hand.

The FGPMMOPA6H chips can be found [at Adafruit](https://www.adafruit.com/products/790) or [on Alibaba](https://www.alibaba.com/showroom/fgpmmopa6h.html).

|Ref|Qty|Description|Digikey PN|
|---|---|-----------|------|
|AN1|1|CONN UFL JACK STR 50 OHM SMD|H122041-ND|
|BAT1|1|CR1220 BATTERY HOLDER SMT FLATPIN|BK-916-CT-ND|
|C3 C2 C1|3|CAP CER 1UF 10V X7R 0603|1276-1946-1-ND|
|C4|1|CAP CER 0.01UF 50V X7R 0603|490-1512-1-ND|
|D1|1|DIODE GEN PURP 75V 250MA BAS16 SOD323|BAS16WS-E3-08CT-ND|
|J1|1|HEADER MALE 10POS TH 1x10 0.1”|952-1902-ND|
|LED1|1|LED AMBER DIFFUSED 0603 SMD|475-2712-1-ND|
|R1|1|RES SMD 10K OHM 1% 1/8W 0603|RNCP0603FTD10K0CT-ND|
|R3 R2|2|RES SMD 470 OHM 5% 1/4W 0603|RHM470DCT-ND|
|S1|1|SWITCH TACTILE SPST-NO 0.05A 12V|SW1020CT-ND|
|U1|1|IC REG LDO 3.3V 0.15A SOT353|576-3193-1-ND|

|Ref|Qty|Description|Adafruit PN|
|---|---|-----------|------|
|U2|1|GPS MODULE PA6H MTK3339|790|

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-9wXJrcX/0/O/i-9wXJrcX.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-7BPGtzs/0/O/i-7BPGtzs.png">

<img src="https://photos.smugmug.com/Projects/Breakout-Boards/n-Sp9mRP/i-59FfDdX/0/O/i-59FfDdX.png">

