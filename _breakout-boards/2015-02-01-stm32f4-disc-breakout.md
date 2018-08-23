---
layout: hardware
title: STM32F4 Discovery Breakout
description: 
type: project
destination: wickerbox-electronics
category: breakout-boards
subcat: 
location: Oregon
image: /img/thumbs/stm32breakout.png
permalink: 
publish: yes
---

The STM32F4-Discovery development board has columns of male pin headers but arranged so that you can't plug the dev board into a breadboard. This breakout board was handy but cost prohibitive at $40 for three boards. Still, we're open sourcing it just in case someone finds it useful.

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-TV7kmhd/0/L/stm32-v2-side-L.png">

The boards are <a href="https://oshpark.com/shared_projects/LSHOUKpw">shared at OSH Park</a>.

The board is made in Eagle, starting with Jason Lopez's <a href="http://www.electro-tech-online.com/threads/stm32f4-discovery-eagle.123047/">STM32F4-Discovery Board Eagle schematic and footprint</a>.

For the first test, to be machined on an LPKF router, all the traces were placed on the bottom of the board. The bottom copper in the layout here is in blue. We didn't want to have to plate all the via holes by hand to solder on the bottom and use traces on the top. Been there, done that, not interested. There are 200 vias on this board!

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-gTFtSPm/0/L/stm32f4-v1-layout-L.png">

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-nD3cv57/0/L/stm32-top-separate-L.png">

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-55T6mm6/0/L/stm32-v1-top-L.png">

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-k5PXQ8G/0/L/stm32-side-L.png">

It worked fine, but there's no silk, so we uploaded the now-verified Eagle .brd file to OSH Park. At $5/sq inch for a set of three, it was $53.05 for three! Way out of the price budget. Luckily, you can submit designs where two completely separate boards are sitting next to each other on one .brd file.

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-HQp3R2h/1/L/stm32-v2-layout-L.png">

This is the OSH Park preview with a cost of $33.95 for three. OSH Park charges for the smallest rectangle that encompasses your design, and you have to leave 100 mils between boards so the fab can mill it out.

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-KgQF7gt/0/L/osh-preview-L.png">

It's still significant, at about $10/board, but possibly worth the hassle. The 2x25 and 1x25 female headers also added up. The boards look great, though.

<img src="https://jenner.smugmug.com/STM32-Discovery-Breakout/i-JKpjxKg/0/L/stm32-v2-closeup-L.png">

The design is licensed under CERN's Open Hardware License v1.2.

The design files are available at the <a href="https://github.com/wicker/stm32f4-discovery-breakout-board">Github repository</a>, and the boards can be ordered <a href="https://oshpark.com/shared_projects/GJyFucOY">for $33.95 for a set of three from OSH Park</a>.

We used these Sullins female headers, and there may be cheaper equivalents.  

Qty 4 of <a href="https://www.digikey.com/product-detail/en/PPTC251LFBN-RC/S7023-ND/810163">PPTC251LFBN-RC</a> 1&#215;25 0.1&quot; for $1.41 each<br />Qty 2 of <a href="https://www.digikey.com/product-detail/en/SFH11-PBPC-D25-ST-BK/S9201-ND/1990094">SFH11-PBPC-D25-ST-BK</a> 2&#215;25 0.1&quot; for $2.89 each.

