---
layout: hardware
title: What my output looks like
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

I'm a freelance hardware developer and I create boards for other people, so it's incredibly important that I'm communicating clearly at every step of the process. It also means I might build a set of boards by hand in my lab, or I might work with a contract manufacturer for a small production run. 

Every client and board house is a little different and I certainly don't want to be spending hours setting up files or run the risk of mixing things up, so I set up and use KiCad templates. I also run KiCad on Linux Mint with Python scripting turned on, and I have a script called Kifisher to take the .net netlist and the board layout to create all these outputs. I use Pandoc to create the PDF, GerbV for processing the manufacturing layers, and imagemagick for the preview images.

The main place everything gets collected is in a git repository on Github. I keep private repos for my closed source client work and public repositories for my open source work. The files KiCad works on are all just text files so they're very readable and easily parsable in the version control. 

Here's an example of the outputs of a <a href="https://github.com/wickerbox/Basic-Breakout-Boards/tree/master/fgpmmopa6h-gps-breakout">GPS breakout board</a>. This design is closely modeled on a perennially out-of-stock design from Adafruit. After buying and prototyping a couple of their breakout boards, I realized I needed an adjusted design of my own. 

As you can see, the README on the front page of the repository has all the information and diagrams in one place. My username is `wicker` and this is the `wickerbox` organization for Wickerbox Electronics.

I always put a photo of an assembled board at the top, if only to jog my memory. That's followed by any notes or more detailed project background information.  

![Git Repo](/img/kicad/outputs-gitrepo.png)

If it's not too detailed or complicated, I'll include a screenshot of the schematic. The repository always includes a full printable PDF on US Letter (8.5x11") size paper. Here's a (<a href="https://github.com/wickerbox/Basic-Breakout-Boards/raw/master/fgpmmopa6h-gps-breakout/fgpmmopa6h-gps-breakout-v1.1.pdf">link</a>). 

![Schematic](/img/kicad/outputs-schematic.png)

I always include the company information on my template so I never have to load it at the start of a project. 

![Company Info](/img/kicad/outputs-gps-company-info.png)

The README includes a bill of materials written in Github Markdown. 

I also make a master, fairly readable .csv file along with individual .csv files in a form that's uploadable to each vendor (such as Digikey or Seeed), and I'll sometimes create a shareable cart and link that directly. 

![Bill of Materials](/img/kicad/outputs-bom.png)

The preview image is still a work in progress, but it gets the idea across. 

![Preview](/img/kicad/outputs-preview.png)

The manufacturing files can be opened in a gerber viewer such as GerbV. 

I include the individual files in a subfolder called `gerbers` but also provide a zipped `name-v1.2-gerbers.zip` archive. 

![Gerbers](/img/kicad/outputs-gerbers.png)

One of the gerber layers included in that file is called FabNotes.gbr. I've switched up the colors here so it's readable. It's created from the board outline, the drill report, and the Dwgs.User layer where I placed the fabrication notes test box. 

Some vendors, such as OSH Park, completely ignore this file because they have a streamlined process where they tell you what their service will provide. Other vendors have tons of services and want to know what you're looking for. 

It also helps for error checking, so the CAM engineer can pause the process and get in touch if they notice you included four copper layers but this file says 'This is a 2 layer board.'

![Fab Notes](/img/kicad/outputs-fabnotes-gerber.png) 

The stencil files are the paste layers from that `gerbers` file along with the board outline, so they can also be opened in a gerber viewer. I include these files in a zipped `name-v1.2-stencils.zip` archive that can be uploaded to something like OSH Stencils. 

![Stencil](/img/kicad/outputs-stencils.png)

The assembly diagram is most useful for me sitting at my desk placing parts, but it can be useful for double checking at a contract manufacturer. Shown here are the really common lines to indicate cathodes and cut corners or circles to indicate a pin 1, but additional notes are incredibly valuable. 

For example, the bottom assembly diagram doesn't give enough information about which way to place the battery holder if you're using one that's not bidirectional. 

I create these assembly diagrams automatically from the Fab and Edge.Cuts (outline) layers. All of my footprints have this information on their F.Fab layer so there's no extra work involved when I prepare the manufacturing files.  

![Assembly Diagram](/img/kicad/outputs-assembly.png)

The final zip file that I would send to a manufacturer includes the output PDF, the gerbers zip, the stencils zip (if this is a surface mount design), and one or more versions of the bill of materials.

You can [view or fork the repository at Github](https://github.com/wickerbox/Basic-Breakout-Boards/tree/master/fgpmmopa6h-gps-breakout).
