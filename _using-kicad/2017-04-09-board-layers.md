---
layout: hardware
title: Board Layers
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

One of the first things to know about footprints and the board layout is how KiCad handles the different layers. These layers will be used in manufacturing to tell the board house where to place copper, where to remove mask, and so on.

In PCBNew and in the Footprint Editor, there's a `Visibles` menu on the righthand side of the screen. It has two tabs: `Layer` and `Render`.

My default template hides a lot of the assembly-related layers in the `Layer` tab, since I'm only interested in the basic layers that I need to get the board fabricated. If I were doing even a small production run, I'd be paying attention to those other layers to help guide the assembly process. 

The `Render` tab is useful for turning on and off things like pads, different kinds of vias, the unrouted wires (ratsnest), the grid, and other things. It's good to know it's there when something's gone missing. 

These are the layers I use:

![](/img/kicad/layers-visiblesmenu.png)

### Throwie Example Project 

I created an example project to show the different layers in KiCad, GerbV, the OSH Park previews, the OSH Stencils previews, a real stencil, a bare board, and an assembled board. 

This is a simple 'throwie' with a surface mount holder for a coin cell battery and a through-hole LED. Here's the circuit:

![Throwie circuit](/img/kicad/throwie-schematic.png)

### Finished Product

![Finished Top](/img/kicad/throwie-final-top.png)

![Finished Bottom](/img/kicad/throwie-final-bottom.png)

There's a lot going on here, so we'll go layer by layer.

It's important to note that KiCad lets you look down the layers as if they were all viewed from the top, so text on the bottom of the board should appear reversed. This purple OSH Park preview displays the bottom of the board as if it were the finished board you were holding in your hand.

### Copper Layers

The fabrication house starts with a piece of copper-clad material and then removes copper to leave only what is indicated on the copper layers. 

F.Cu (the red layer in KiCad) is the top copper layer and B.Cu (the green layer in KiCad) is the bottom copper layer.

<img src="/img/kicad/throwie-top-copper.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-bottom-copper.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

### Mask Layers

F.Mask and B.Mask are top and bottom mask layers, and they are also negative layers. The mask is a film that only has openings where you want to apply solder, so you can cover traces and protect yourself from shorting across signals with solder.

To get gold or silver text (depending on your chosen board finish), you can leave openings in the mask over copper or over the bare substrate. Compare the results of the `Light!` and `No Light :(` text.

<img src="/img/kicad/throwie-top-mask.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-bottom-mask.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

Also, notice the drill hits for the through-hole LED. The LED will be soldered from the bottom so the copper pads need to be exposed on the bottom. The copper pads must be present on the top to connect to the copper traces and to provide stability for the copper plating on the inside of the drill hole between top and bottom, but those pads don't need to be exposed.

<img src="/img/kicad/throwie-top-drills-mask-copper.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-bottom-drills-mask-copper.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

### Silkscreen Layers

F.SilkS and B.SilkS are the top and bottom silkscreen layers, which are applied to the board at the end of the process. These layers are optional but very useful. 

<img src="/img/kicad/throwie-top-silk.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-blank-layer.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

### Paste Layers

F.Paste and B.Paste are the top and bottom paste layers. These are negative layers, which means any rectangles or other features will be where a hole will be cut in a stencil. This is so you can place a stencil over the top of the board and smear paste only on the exposed copper pads. 

<img src="/img/kicad/throwie-top-paste.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-top-stencil.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

### Fab Layers

I use the F.Fab and B.Fab layers for the assembly diagram information. 

<img src="/img/kicad/throwie-top-fab.png" style="width: 45%; float:left;">

<img src="/img/kicad/throwie-blank-layer.png" style="width: 45%; float:right;">

<div style="clear:both;">&nbsp;</div>

### Drills Layer

The Excellon drill file contains all the information the manufacturing machines need to know about where (which coordinates) to place the drill holes and what tool diameter is needed for each hole. Some newer services, like OSH Park, use this information to place drills and they don't need an older-style drill map.

KiCad places these holes automatically when you place a through-hole pad. Holes are plated by default.

To specify an unplated hole, select `Mechanical, NPTH` for the Pad Type and `Circular` for the Shape. Make the `Drill Size X` the same size as the `Size X` for the pad.

<img src="/img/kicad/throwie-drills.png" style="width: 45%; float:left;">

<div style="clear:both;">&nbsp;</div>

### Fab Notes

KiCad will create a drill map gerber in a human-readable format, though where it puts the text is sometimes a little unpredictable. I add my fab notes as a piece of text on the Dwgs.User layer when I'm finishing up the board.

It sometimes takes a couple of tries, moving the board and text around, to get the Dwgs.User, drill drawing, and Edge.Cuts layers to not overlap each other. Once that's there, I merge those three layers into one gerber that ends in -FabNotes.gbr.

What exactly I write on my fab notes depends on the fabrication house I'm going to use to make the boards. OSH Park, for example, doesn't pay any attention to these files because it's a prototyping service with one standard offering. Other services with more options are more likely to use the fab notes and get in touch with you if somethingon the fab notes doesn't make sense.

![](/img/kicad/throwie-fab-notes.png)

### Adding a Pad to a Footprint

Adding a pad to a footprint will come with something on the copper, mask, and paste layers by default. You can turn on or off the layers in the item's property menu.

This is a circular drill with a 1.016mm diameter. The pad number is `1` and the pad is a square that's 2.032mm across. This hole will have copper plated on the inside of the hole so the signal on the top of the board can be passed on to inner layers or to the bottom side. 

The checkboxes indicate this pad will show up on the Mask layers on both sides, so the whole pad will be exposed on the top and bottom. 

If you know you'll only be soldering on the bottom, it's fairly common to only check `B.Mask` so there is only an opening in the mask on the bottom.  

![](/img/kicad/layers-pad.png)

