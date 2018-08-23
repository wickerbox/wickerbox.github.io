---
layout: hardware
title: Carb Sync Shield
description: Carb sync Arduino shield for motorcycles. 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/carbsync.png
permalink: 
publish: yes
---

We worked with Tom Hogue over at [Digital Carb Sync](https://digitalcarbsync.com/) to translate his prototyped breadboard design onto a printed circuit board. He's done all of the software; our contribution was entirely in hardware. 

The Carb Sync Shield monitors the up to six carburetors and displays the vacuum pressure in realtime on an LCD display so the user can make adjustments to the air/fuel mix in each cylinder.

There's an additional RPM feature that will be useful to set and monitor the idle speed on bikes that don't have a tachometer.

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-CnTJMHR/0/L/IMG_2190-L.jpg">

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-JPjRQ3X/0/L/IMG_2193-L.jpg">

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-895ngdv/0/L/IMG_2433-L.jpg">

The kit can be assembled by a novice using a basic soldering iron. The pressure sensors have extra-large surface mount pads and all other components are through-hole. 

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-NcsHnpf/0/M/IMG_2304-M.jpg">

The shield is compatible with both the <a href="http://store.arduino.cc/product/A000066">Arduino Uno v3</a> and the Bluetooth-capable <a href="http://redbearlab.com/blend/">RedBear Blend v1</a>. It displays the RPM calculated from each of up to six simultaneous 3.3V or 5V pressure sensors on an LCD display which can be mounted directly or connected with the rainbow jumpers as shown above. 

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-PCbRQZg/0/M/ardblend-M.png">

The board draws power from the carrier Uno or Blend board, which in turn can run off a 9V battery or a USB plug. The blue trim potentiometer controls the brightness of the LCD so it's visible indoors or outdoors. The large switch sets the analog pressure sensor reference voltage to 3.3V or 5V. In the final version of the board, the switch is replaced with a 3-pin header and jumper cap.  

Three digital I/O lines are broken out along with dedicated 5V or 3.3V pins to support extra sensors. It's up to the user to match the sensor voltage on the digital line to the expected operating voltage of the Uno or Blend.

We had the boards fabricated through <a href="http://oshpark.com">OSHPark</a>, a local batch PCB service based in Oregon, and did a successful test in early November on Tom's bike. 

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-BJjknMv/0/L/IMG_2436-L.jpg">

<img src="https://jenner.smugmug.com/Carb-Sync-Shield/i-t9DcvPN/0/L/IMG_2438-L.jpg">

