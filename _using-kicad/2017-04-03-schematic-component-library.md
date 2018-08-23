---
layout: hardware
title: Schematic Symbol Library 
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

A schematic consists of symbols representing physical parts connected by green and blue signal lines.

![](/img/kicad/powerflags.png)

Each symbol (also called a component) has its own unique definition in the component libraries.

![](/img/kicad/symbols-symbol.png)

KiCad ships with a bunch of default schematic component libraries. Each component has a picture drawing and some attached information like the reference designator (C1), value (10uF cap), datasheet (html link), and footprint name.

Managing lots of different libraries is the hardest part of using KiCad, so I decided to build a single library of components. 

### Why

I want to set this up and never think about it again. I want to make hundreds of boards. 

- BOM Auto output
- Never enter info by hand in the schematic
- Reuse parts that I have in stock

### Single Library

I call my library wickerlib. All the component information lives in two files: `wickerlib.dcm` and `wickerlib.lib`.

### Adding the Library to the Project Template

I use templates for new projects so I never have to edit the list of libraries by hand at the beginning of a project. I have to edit the template .pro and the .sch files to get the library linked properly.

I've edited the `project.pro` file to point to my wickerlib library on my computer. That folder contains the .lib and .dcm files.

```
[eeschema]
version=1
LibDir=/home/wicker/wickerlib/libraries/
[eeschema/libraries]
LibName1=/home/wicker/wickerlib/libraries/wickerlib
```

In the .sch file, I replace all the LIBS: lines with one, as shown:

```
EESchema Schematic File Version 2
LIBS:wickerlib
EELAYER 25 0
EELAYER END
```

If there are no libs specified, KiCad seems to error every time you open the schematic file because it falls back to looking for its default libraries.

![Missing library](/img/kicad/symbols-missinglib.png)

I do back up the wickerlib folder in a git repository, but I like to work offline so I don't get the library from Github automatically through KiCad. As far as KiCad is concerned, my libraries live in local folders on the same computer as KiCad. 

### Wickerlib

Here's an example of how KiCad uses a library component from the library definition to the schematic. 

A component is defined in wickerlib.dcm and wickerlib.lib files, which are just text files so they're easy to read and edit. 

The $CMP lines should match between the .dcm and .lib files. 

The .dcm file just consists of a list of all the component names in the library, along with a couple of optional fields for description and datasheet. I only use the description line because that's how KiCad lets you search for the part when you `add` a component in the schematic.

```
#
$CMP IC-MCU-ATMEGA328-TQFP32-CUSTOM1
D IC MCU 8BIT 32KB FLASH 32TQFP
$ENDCMP
#
```

The .lib file specifies the symbol picture to place on the schematic and a set of informational fields. The first four of these are required. 

- F0 - Reference Designator
- F1 - Full symbol value
- F2 - Footprint
- F3 - Datasheet link

```
#
# IC-MCU-ATMEGA328-TQFP32-CUSTOM1
#
DEF IC-MCU-ATMEGA328-TQFP32-CUSTOM1 U 0 40 Y Y 1 F N
F0 "U" -750 1250 50 H V L CNN
F1 "IC-MCU-ATMEGA328-TQFP32-CUSTOM1" 850 -1350 50 H V R CNN
F2 "Wickerlib:TQFP-32-7x7MM-P0.8MM" 0 -350 50 H I C CIN
F3 "http://www.atmel.com/images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet_Complete.pdf" 0 0 5 H I C CNN
F4 "IC MCU 8BIT 32KB FLASH 32TQFP" 0 -350 50 H I C CIN "Description"
F5 "Atmel" 0 -350 50 H I C CIN "MF_Name"
F6 "ATMEGA328P-AU" 0 -350 50 H I C CIN "MF_PN"
F7 "Digikey" 0 -350 50 H I C CIN "S1_Name"
F8 "ATMEGA328P-AU-ND" 0 -350 50 H I C CIN "S1_PN"
DRAW
S -750 1200 850 -1300 0 1 10 N
X (PCINT19/OC2B/INT1)PD3 1 1000 950 150 L 40 40 1 1 B
X (PCINT20/XCK/T0)PD4 2 1000 850 150 L 40 40 1 1 B
X GND 3 -350 -1450 150 U 40 40 1 1 W
X VCC 4 -300 1350 150 D 40 40 1 1 W
X GND 5 -450 -1450 150 U 40 40 1 1 W
X VCC 6 -200 1350 150 D 40 40 1 1 W
X (PCINT6/XTAL1/TOSC1)PB6 7 -900 250 150 R 40 40 1 1 B
X (PCINT7/XTAL2/TOSC2)PB7 8 -900 -50 150 R 40 40 1 1 B
X (PCINT21/OC0B/T1)PD5 9 1000 750 150 L 40 40 1 1 B
X (PCINT22/OC0A/AIN0)PD6 10 1000 650 150 L 40 40 1 1 B
X AREF 20 -500 1350 150 D 40 40 1 1 B
X (PCINT16/RXD)PD0 30 -900 -650 150 R 40 40 1 1 B
X (PCINT23/AIN1)PD7 11 1000 550 150 L 40 40 1 1 B
X GND 21 -550 -1450 150 U 40 40 1 1 W
X (PCINT17/TXD)PD1 31 -900 -800 150 R 40 40 1 1 B
X (PCINT0/CLKO/ICP1)PB0 12 1000 450 150 L 40 40 1 1 B
X ADC7 22 1000 -1200 150 L 40 40 1 1 I
X (PCINT18/INT0)PD2 32 1000 1050 150 L 40 40 1 1 B
X (PCINT1/OC1A)PB1 13 1000 350 150 L 40 40 1 1 B
X (PCINT8/ADC0)PC0 23 1000 -500 150 L 40 40 1 1 B
X (PCINT2/OC1B/~SS~)PB2 14 1000 250 150 L 40 40 1 1 B
X (PCINT9/ADC1)PC1 24 1000 -600 150 L 40 40 1 1 B
X (PCINT3/OC2A/MOSI)PB3 15 -900 550 150 R 40 40 1 1 B
X (PCINT10/ADC2)PC2 25 1000 -700 150 L 40 40 1 1 B
X (PCINT4/MISO)PB4 16 -900 450 150 R 40 40 1 1 B
X (PCINT11/ADC3)PC3 26 1000 -800 150 L 40 40 1 1 B
X (PCINT5/SCK)PB5 17 -900 650 150 R 40 40 1 1 B
X (PCINT12/SDA/ADC4)PC4 27 1000 -900 150 L 40 40 1 1 B
X AVCC 18 -400 1350 150 D 40 40 1 1 W
X (PCINT13/SCL/ADC5)PC5 28 1000 -1000 150 L 40 40 1 1 B
X ADC6 19 1000 -1100 150 L 40 40 1 1 I
X (PCINT14/~RESET~)PC6 29 -900 750 150 R 40 40 1 1 B
ENDDRAW
ENDDEF
```

I want to automatically capture information for my bill of materials so I added some fields. The fields aren't in any paticular order, since the important information is the rightmost field name in quotes. 

- F4 - Description
- F5 - Manufacturer Name
- F6 - Manufacturer Part Number
- F7 - Source 1 Name
- F8 - Source 1 Part Number

This has singlehandedly saved me more time and grief than any other KiCad workflow decision. 

When the component is added to a schematic, its definition is placed in the .sch file with the appropriate coordinates. 

```
$Comp
L IC-MCU-ATMEGA328-TQFP32-CUSTOM1 U2
U 1 1 586895A2
P 6050 4075
F 0 "U2" H 5300 5325 50  0000 L CNN
F 1 "ATMEGA328" H 6900 2725 50  0000 R CNN
F 2 "Wickerlib:TQFP-32-7x7MM-P0.8MM" H 6050 3725 50  0001 C CIN
F 3 "http://www.atmel.com/images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet_Complete.pdf" H 6050 4075 5   0001 C CNN
F 4 "IC MCU 8BIT 32KB FLASH 32TQFP" H 6050 3725 50  0001 C CIN "Description"
F 5 "Atmel" H 6050 3725 50  0001 C CIN "MF_Name"
F 6 "ATMEGA328P-AU" H 6050 3725 50  0001 C CIN "MF_PN"
F 7 "Digikey" H 6050 3725 50  0001 C CIN "S1_Name"
F 8 "ATMEGA328P-AU-ND" H 6050 3725 50  0001 C CIN "S1_PN"
  1    6050 4075
  1    0    0    -1
$EndComp
```

You can see the schematic only provides a placeholder for the component. This is important! KiCad depends on finding a library 

The real header in the `.sch` file should include the cached local library:

```
EESchema Schematic File Version 2
LIBS:wickerlib
LIBS:atmega328-cache
EELAYER 25 0
EELAYER END
```

This depends on the `atmega328-cache.lib` file that KiCad creates next to the `.sch` file. As long as this file is present (ideally first in the list of LIBS) then KiCad will remember how to draw the symbol. Do not delete this library! I have a policy not to edit existing symbols, just in case, and so I create variants of the symbol that end in -CUSTOM1, -CUSTOM2, etc. Still, this isn't foolproof. 

Leaving the -cache.lib file in place can look messy but it allows you to do things like manually change the part number or edit the symbol locally without affecting the wickerlib library itself.

Like `wickerlib.lib`, the `atmega328-cache.lib` holds all the information needed to draw the part.
```
#
# IC-MCU-ATMEGA328-TQFP32-CUSTOM1
#
DEF IC-MCU-ATMEGA328-TQFP32-CUSTOM1 U 0 40 Y Y 1 F N
F0 "U" -750 1250 50 H V L CNN
F1 "IC-MCU-ATMEGA328-TQFP32-CUSTOM1" 850 -1350 50 H V R CNN
F2 "Wickerlib:TQFP-32-7x7MM-P0.8MM" 0 -350 50 H I C CIN
F3 "http://www.atmel.com/images/Atmel-8271-8-bit-AVR-Microcontroller-ATmega48A-48PA-88A-88PA-168A-168PA-328-328P_datasheet_Complete.pdf" 0 0 5 H I C CNN
F4 "IC MCU 8BIT 32KB FLASH 32TQFP" 0 -350 50 H I C CIN "Description"
F5 "Atmel" 0 -350 50 H I C CIN "MF_Name"
F6 "ATMEGA328P-AU" 0 -350 50 H I C CIN "MF_PN"
F7 "Digikey" 0 -350 50 H I C CIN "S1_Name"
F8 "ATMEGA328P-AU-ND" 0 -350 50 H I C CIN "S1_PN"
DRAW
S -750 1200 850 -1300 0 1 10 N
X (PCINT19/OC2B/INT1)PD3 1 1000 950 150 L 40 40 1 1 B
X (PCINT20/XCK/T0)PD4 2 1000 850 150 L 40 40 1 1 B
X GND 3 -350 -1450 150 U 40 40 1 1 W
X VCC 4 -300 1350 150 D 40 40 1 1 W
X GND 5 -450 -1450 150 U 40 40 1 1 W
X VCC 6 -200 1350 150 D 40 40 1 1 W
X (PCINT6/XTAL1/TOSC1)PB6 7 -900 250 150 R 40 40 1 1 B
X (PCINT7/XTAL2/TOSC2)PB7 8 -900 -50 150 R 40 40 1 1 B
X (PCINT21/OC0B/T1)PD5 9 1000 750 150 L 40 40 1 1 B
X (PCINT22/OC0A/AIN0)PD6 10 1000 650 150 L 40 40 1 1 B
X AREF 20 -500 1350 150 D 40 40 1 1 B
X (PCINT16/RXD)PD0 30 -900 -650 150 R 40 40 1 1 B
X (PCINT23/AIN1)PD7 11 1000 550 150 L 40 40 1 1 B
X GND 21 -550 -1450 150 U 40 40 1 1 W
X (PCINT17/TXD)PD1 31 -900 -800 150 R 40 40 1 1 B
X (PCINT0/CLKO/ICP1)PB0 12 1000 450 150 L 40 40 1 1 B
X ADC7 22 1000 -1200 150 L 40 40 1 1 I
X (PCINT18/INT0)PD2 32 1000 1050 150 L 40 40 1 1 B
X (PCINT1/OC1A)PB1 13 1000 350 150 L 40 40 1 1 B
X (PCINT8/ADC0)PC0 23 1000 -500 150 L 40 40 1 1 B
X (PCINT2/OC1B/~SS~)PB2 14 1000 250 150 L 40 40 1 1 B
X (PCINT9/ADC1)PC1 24 1000 -600 150 L 40 40 1 1 B
X (PCINT3/OC2A/MOSI)PB3 15 -900 550 150 R 40 40 1 1 B
X (PCINT10/ADC2)PC2 25 1000 -700 150 L 40 40 1 1 B
X (PCINT4/MISO)PB4 16 -900 450 150 R 40 40 1 1 B
X (PCINT11/ADC3)PC3 26 1000 -800 150 L 40 40 1 1 B
X (PCINT5/SCK)PB5 17 -900 650 150 R 40 40 1 1 B
X (PCINT12/SDA/ADC4)PC4 27 1000 -900 150 L 40 40 1 1 B
X AVCC 18 -400 1350 150 D 40 40 1 1 W
X (PCINT13/SCL/ADC5)PC5 28 1000 -1000 150 L 40 40 1 1 B
X ADC6 19 1000 -1100 150 L 40 40 1 1 I
X (PCINT14/~RESET~)PC6 29 -900 750 150 R 40 40 1 1 B
ENDDRAW
ENDDEF
```

### Naming Convention

KiCad's default libraries have names like C_small and C because all they think you want is the symbol itself. Every one of my symbols has information for a particular manufacturer part number, so I want a lot more information than that. I end up with a lot of parts so I name them so they're easy to search.

For example, this capacitor is a ceramic 10uF capacitor with a voltage limit of 25V and temperature tolerance rating of X7R. It's a surface mount part of package size 1210. This lets me limit keystrokes whne I'm trying to add a part. 

I type `a`, then `CAP CER` or `CAP 1210` or `CAP 50V` or `CAP 10uF 1210` to see all my options. 

![](/img/kicad/symbols-componentselection.png)

Parts in my library are there because I've used them before, and I probably have a few left over since I try to round up to the next volume discount level. If I don't have the part I need (different package size, etc) then I usually select one that's close enough and place it on the schematic.

### Creating the New Part

Once the new part is placed, I click `Ctrl+e` to open my Part Library Editor.

Hopefully, the library is already indicated as being wickerlib:

![](/img/kicad/symbols-libraryname.png)

If it isn't, I go to `File > Current Library` and click `wickerlib`.

The component visual representation usually looks like this:

![](/img/kicad/symbols-saveas.png) 

There's the reference designator and value visible on the part. The datasheet is a tiny field at the origin, and the rest of the gray text are the invisible field names that are present in the component but won't be visible on the schematic.

Let's say I'm creating an 18pF 16V 0603 capacitor to use with a crystal. The very first thing to do is create a new component by saving this one as a new name. I start by hitting `e` on the `CAP-CER-10UF-16V-X7R-0805` symbol. I enter in the new symbol value in the text box and click `OK`. 

![](/img/kicad/symbols-newname.png)

This action created new entries in `wickerlib.lib` that have the new name but otherwise the exact same internal information as the previous component. We'll want to update those values. 

I go off and collect the manufacturing information I need, find a vendor for the part, and then one at a time I hit `e` on each of the gray values and replace them with the new information. This will update all the field lines in `wickerlib.lib`.

If you stopped now, this componet wouldn't show up when you tried to `add` it because the description in `wickerlib.dcm` is still the original CAP-CER-10UF... description. The final fix is to click on the `Edit component properties` box with the little gear.

![](/img/kicad/symbols-editcomp.png)

Update the description so the schematic will be able to find it.

![](/img/kicad/symbols-description.png)

There are also some other options, such as if you want pin numbers to show. This is valuable for parts with lots of pins but it makes capacitor symbols very cluttered.

![](/img/kicad/symbols-options.png)

Once that's done, using the part is just a matter of a few keystrokes and a click to place it. 

I'll talk about linking a footprint later.

### Using the Schematic Parts Editor

The user interface and hotkeys are very similar to the schematic editor.

- `g` grabs and lets you move the side of a box
- `m` moves things
- `p` adds pins
- `r` rotates things

The default grid in KiCad is 0.05" (50 mils) so I stick with that or 0.1" (100 mis) for all of my created parts so there's no conflict in EESchema with a 0.05" grid. If the parts are created with 0.05" pin spacing and EESchema is set to use 0.1" (which was what I always used in Eagle), then wires might not be able to be hooked up to pins because of the grid offset. 

There don't appear to be any hotkeys to draw boxes, but you can resize boxes with the `g` grab tool. The graphics here are somewhat limited. 

KiCad doesn't really care about the pin names, so I usually just match them to the datasheet. What KiCad <em>really</em> cares about is the pin numbers, though it doesn't matter until I'm actually associating footprints. But it really matters then.  

On giant parts, it's handy to batch import pins from a spreadsheet, but I havn't figured out how to do that yet. There's an option to hide power pins, but for now I like to have all the pins visible. 

Since the number of symbol pins have to match the number of pads in the footprint, there's a visual trick where you can stack sets of pins that are the same on top of each other. This can be handy for GND or VCC pins, but I like to see at a glance what all my pins are doing, so I leave them separate. 

Keep in mind that the pin numbers connect a symbol to its footprint; adding labels to the traces will allow you to see that trace name on the layout while you're routing traces to connect different packages together. The pin number on one package does not have to match the pin number on another package!
