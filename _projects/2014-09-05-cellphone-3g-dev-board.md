---
layout: hardware
title: DIY Cellphone 3G Build
description: Updating the 2G DIYCellphone to use a 3G module. 
type: project
destination: wickerbox-electronics
category: projects
subcat: 
location: Oregon
image: /img/thumbs/cellboard.png
permalink: 
publish: yes
---

<img src="https://jenner.smugmug.com/3G-Cellphone/i-vmwWrZq/0/L/finalboard-L.jpg">

<a href="http://web.media.mit.edu/~mellis/">David A Mellis</a> designed a <a href="http://web.media.mit.edu/~mellis/cellphone/">DIY 2G Cellphone</a> using the Quectel GSM/GPRS M10 2G module and the Arduino GSM Shield library. We updated David’s design with his permission and replaced the M10 with a Quectel UMTS/HSDPA UC15 3G module.

The modules have different pinouts, slightly different packages, and the UC15 takes 3.3V-4.3V while the M10 took 3.3V-4.6V, which accommodates a 3.7V LiPo battery.

We got the boards back and did an initial build, then handed things over to a local software developer who developed and <a href="https://www.youtube.com/watch?v=FlRa-iH7PGw">presented the working cellphone at !!Con</a>.

The Eagle schematic and layout, along with the development notes and bill of materials are available for the first version of the hardware at <a href="https://github.com/wicker/cellphone3g">its GitHub repo</a>. The project is released as open hardware under the MIT license.

<img src="https://jenner.smugmug.com/3G-Cellphone/i-xWbgKFF/0/X2/board-X2.png">

<strong>Vocabulary</strong>

- GSM - Global System for Mobile Communications, 2G
- GPRS - General Packet Radio Services, packet data service on 2G and 3G
- UMTS - Universal Mobile Telecommunications System, 3G
- HSDPA - High-Speed Downlink Packet Access, allows higher speeds 3G speeds**

<strong>Reference</strong>

"GSM (Global System for Mobile Communications, originally Groupe Spécial Mobile), is a standard developed by the European Telecommunications Standards Institute (ETSI) to describe protocols for second generation (2G) digital cellular networks used by mobile phones." <a href="http://en.wikipedia.org/wiki/GSM">Wikipedia</a>

"General packet radio service (GPRS) is a packet oriented mobile data service on the 2G and 3G cellular communication system's global system for mobile communications (GSM)." <a href="http://en.wikipedia.org/wiki/General_Packet_Radio_Service">Wikipedia</a>

"UMTS specifies a complete network system, which includes the radio access network (UMTS Terrestrial Radio Access Network, or UTRAN), the core network (Mobile Application Part, or MAP) and the authentication of users via SIM (subscriber identity module) cards." <a href="http://en.wikipedia.org/wiki/Universal_Mobile_Telecommunications_System">Wikipedia</a>

"High-Speed Downlink Packet Access (HSDPA) is an enhanced 3G (third-generation) mobile-telephony communications protocol in the High-Speed Packet Access (HSPA) family, also dubbed 3.5G, 3G+, or Turbo 3G, which allows networks based on Universal Mobile Telecommunications System (UMTS) to have higher data-transfer speeds and capacity." <a href="https://github.com/wicker/cellphone3g/blob/master/en.wikipedia.org/wiki/High-Speed_Downlink_Packet_Access">Wikipedia</a>


