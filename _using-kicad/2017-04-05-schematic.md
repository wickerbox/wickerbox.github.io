---
layout: hardware
title: Schematic Editor
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

I used a template so my Electrical Rules Checker is already set properly, and the schematic is initialized with a grid in Inches with spacing of 50 mils. 

The last thing before starting the schematic is to go to `File > Page Settings` and add in the Issue Date, Revision, and Title. Everything else is already filled in so I don't have to worry about it.

<img src="/img/kicad/page-settings.png">

What this does is fill in the lower right-hand corner box with my information for this schematic. I only have to do this once, I immediately feel very professional and legitimate, and I never have to worry about it again. 

<img src="/img/kicad/worksheet-settings.png">

<hr>

##### Custom Hotkeys

The KiCad libraries are excellent and have a lot of what I need, so I've been using them for most components. They're added in much the same way as Eagle with the `a` key.

I hate moving my hand back and forth from the keyboard to the mouse to click, so I use my laptop touchpad to hover the mouse and hotkeys for all the actions, like grabbing, placing wires, or adding labels. 

I've been slowly mapping hotkeys to be entirely left hand, so I can use my right on the touchpad and everything else with the left.

To that end, the very first hotkey I suggest changing is removing a component form `Delete` to `d`. 

The other one that is invaluable is holding down `shift` when you select a group of parts. That allows you to drag them as a group.

My other hotkey notes

- `d`   deletes a part
- `shift+d`  deletes a node
- `a`		adds a part
- `g`   grabs a part along with its connected wires
- `m`		moves a part separate from its connected wires
- `r`		rotates a part
- `w`		adds a wire
- `l`	  adds a label, effectively naming a net
- `x`		flips part across x axis (up/down)
- `y`		flips part across y axis (left/right)

<hr>

##### Frustrating Differences from Eagle

Like a lot of people, I started out using Eagle and ran into some confusing differences. For one thing, the schematic editor is actually a program of its own called EESchema that's wrapped up in KiCad, so it can be launched on its own from the command line. I'm basically never doing that; I'm afraid of breaking the links between the schematic and layout, for example, so I always launch the editor programs from inside KiCad.

For another, you can't just type full names of things in a command line bar at the top of EESchema like you could in Eagle.There's no way to type `grid inch` or `grid 0.01` to swap the grid from metric to inches or to set it to a grid of 10 mils, for example. There aren't even hotkeys, so you're forced instead to click the mouse for some of the meta settings changes. 

In this case, a right click gives you the option to change the grid. 

Also, the KiCad grid default is 0.05" (50 mils) which can be a shock when you're used to using 0.1". It's best to stick with 0.05" in EESchema because lots of the default component symbols are created using that spacing and if you're using 0.01" it's possible to end up being unable to match wires to pins in the EESchema grid. 

Another big difference is that `m` to move a part won't automatically bring along the rest of the attached wires. For that, you need to think of the grab tool, `g`, as equivalent to the `move` tool of Eagle.

Now, crazily, I'm tempted to explore using `End` and `Return` for mouse clicks. I could see that allowing me to keep all ten fingers on the keypad for touch typing, and just drop a thumb to the touchpad for mouse positioning. But muscle memory of the mouse click is strong, so...

Hitting `Ctrl` before selecting will let you drag and keep wires attached. To move a wire, right click and hit `break wire` and then use `Ctrl` to select and drag that wire. 

Preset trace names were really useful, since I could map them to Power and Default trace settings.

I have to explicitly add wires/connections. Can't just move parts and overlap them and pull them away. That's annoying.

When I need to edit or add a part, I'm careful to only open the Part Library Editor from inside EESchema. Having an established flow makes it less likely I'll make a mistake later when I'm in a rush, tired, or not paying attention.

<hr>

##### Using the new Symbols

If it was a new library, EESchema (being a separate program and all) doesn't know that there's a new library. I have to go to `Preferences > Component Libraries` and `Add` it to the list.

If it was just a part added to an existing library, EESchema will update automatically when I use the `a` hotkey to look for components to add.

<hr>

##### Power Flags

This is a little odd but KiCad's electrical rules checker (ERC) expects each power rail and each ground/return rail to be marked somewhere with a Power Flag. This isn't the usual ground or vcc flag, which I use all over the place, but it's an additional symbol accessible in the same menu that's literally called PWR_FLAG. 

A power rail is also called a power net, and it includes all the instances of that signal everywhere in the schematic. In the image below, I only have to put one power flag on each power net. I have two PWR_FLAGs, one each on`+5V` and `GND`, but the second instance of +5V doesn't need a flag since that net already has one. 

I usually leave placing this for last, to satisfy the rules checkers, since I ususally end up tweaking the schematic placement quite a bit and extra symbols are just annoying to keep track of.

There's also a convention in schematics to always place a junction where more than two wires meet, but never have more than three wires meet there.

<img src="/img/kicad/powerflags.png">

<hr>

##### Text

I don't see enough text around open source schematics on the web, so I just want to point out that the point of a schematic is to functionally describe the circuit so someone else can go and (with the help of the datasheets) lay out the board separately from the original schematic designer.

To that end, I like adding text (sometimes as a note to myself!) to remind myself what I was thinking. Clear, simple explanations can save a lot of hassle later.

This is the same schematic as used above with the power flags, but note that I only had to add a PWR_FLAG to the GNDA rail. I already have one on the +5V and the GNDD rails. Just use one per net! 

<img src="/img/kicad/text.png">

<hr>

##### Running the ERC

Do it! 

