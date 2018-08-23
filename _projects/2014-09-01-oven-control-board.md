---
layout: hardware
title: Oven Control Board
description: Oven controller to make the oven more like an applicance.
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/ovenboard3.png
permalink: 
publish: yes
---

## First Version

An ME capstone team at Portland State is working on an oven so we can cure our own composites. It's awesome. The first version of this board was a quickturn project designed, machined, and assembled in four days. 

The electrical team member already had the design figured out and working with breadboard components and an Arduino, and what he really wanted was an Arduino shield. We met, looked over his work so far, and figured out the rough placement of parts in the space of a shield. 

This is his schematic in Eagle.

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-Grcj9cH/0/O/i-Grcj9cH.png">

The very first thing we did was to redraw the schematic to give a better sense of the functional flow of signals and power through the circuit. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-d53LZHG/0/O/i-d53LZHG.png">

The layout was constrained by the shield layout but even moreso by our plan to use the LPKF router to machine the board in-house. The boards had to be two layers with no plated through-holes or vias. We placed all the traces except one on the bottom layer because all the components were through-hole and would be soldered on the bottom side. The remaining signal on the top only required two large vias. 

Unfortunately, Arduino shields sit on top of the Arduino and are soldered to the top of the board so we had to drop an extra via on each pad of the 0.1" headers so copper wire could be slid through and squashed, essentially plating the holes by hand. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-Dx3v2DZ/0/O/i-Dx3v2DZ.png">

The final product was functional but the isolation between the copper pads and the rest of the copper ground plane was so small that it made soldering a stressful chore. We electrically verified everything with a multimeter to make sure we hadn't accidentally bridged to cause a short, and handed it off to the mechanical engineers for testing. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-nqnJtKL/0/O/i-nqnJtKL.png">

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-hPRVMpg/0/O/i-hPRVMpg.png">

## Version 2 

The team needed some changes after their testing, including adding a second relay, so the first order of business was editing the schematic. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-pNsZGPz/0/O/i-pNsZGPz.png">

We split the traces more evenly between top and bottom layers this time around. The top layer copper is in red and the bottom layer copper is in blue. The white outline shows where the Arduino will sit beneath the board, so you can see the shield extends a bit beyond the Arduino shape.

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-26qbcQp/0/O/i-26qbcQp.png">

Because we were still making this one by hand in the lab, we weren't able to plate the drilled holes for the pins so we added the same small vias touching the pin pads. We would place the pin in the big hole and solder it to one side of the board, then slide a small diameter wire through the tiny via and crimp it down to make a good connection.

This is a closeup of how to call that out in the board layout:

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-smzXxNS/0/O/i-smzXxNS.png">

Again, we performed the minimal soldering and marked it up with instructions before handing it off to the mechanical team to finish installing.

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-FFJGxp5/0/O/i-FFJGxp5.png">

## Final Version

The last step was to take the design from homemade board to a professionally fabricated board. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-H4Xw49D/0/O/i-H4Xw49D.png"> 

We figured out that we wanted to place the thermocouples on the board itself. We developed the final version of the oven controller and installed it on a 4'x8'x4' curing oven at Portland State in the Mechanical Engineering department. 

The schematic became complicated enough that it was too big to easily fit on a screen, so you can click to open a larger view.

<a href="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-td5nbCr/0/O/i-td5nbCr.png"><img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-td5nbCr/0/O/i-td5nbCr.png"></a>

Because were were going to use OSH Park to fabricate the boards, all of the holes could be plated so there was no more need to place vias in pin pads to connect the top and bottom layers. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-gK7CdkD/0/O/i-gK7CdkD.png">

The electronics are a three-board stack with an Arduino Uno R3 on the bottom; the custom oven control board set up in the middle with screw-in Euroterminals for start switch, relay, and thermocouple wires; and a 1.8" TFT LCD Shield from Adafruit for the display on top. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-n9B3FwK/0/O/i-n9B3FwK.png">

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-TG92jSd/0/O/i-TG92jSd.png">

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-7dQkTvr/0/O/i-7dQkTvr.png">

The blue case is 3D printed, and it holds both the boards and two relays, with a switch on the front cover. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-hHcvxpm/0/O/i-hHcvxpm.png">

The box is attached to the side of the oven, with an air gap to help protect it from the heat.

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-Kd5vcK4/0/O/i-Kd5vcK4.png">

The display allows the user to program up to nine steps in a temperature profile. Using the joystick to navigate the menu, the user can specify a ramp rate, hold temperature, and hold time. Once all the steps are set, the user should set the relay enable switch to ON and then tell the program to begin running the profile. 

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-SWkDk3G/0/O/i-SWkDk3G.png">

<img src="https://jenner.smugmug.com/Oven-Controller/n-PdZDTM/i-cR8DdzH/0/O/i-cR8DdzH.png">

The program automatically detects which thermocouples are present and uses the temperature as input to a PID loop which controls ramp rate by turning on and off up to four relays which control two heaters, a fan, and a vent.

The code and hardware is available <a href="https://github.com/psas/mme-capstone/">on Github in the 'oven-controller'</a> directory.
  


