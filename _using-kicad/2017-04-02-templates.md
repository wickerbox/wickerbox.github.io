---
layout: hardware
title: Making and Using KiCad Templates
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

This is a part of my series on how I use KiCad, so I recommend reading from the beginning. I set things up a little differently and it may not make sense if you haven't read at least `Outputs` and `Getting Started`.

**This is making a template and using that template.**

**First draft done.**

KiCad templates are incredibly useful because they let you start a new project with all the behind-the-scenes settings already specified. You can just open the file and start designing. 

New KiCad projects include a project file (.pro), a schematic file (.sch), and a board layout file (.kicad_pcb), along with some optional extras like a footprint library table (fp-lib-table) to tell KiCad where to find your footprints. 

All of these files can be edited in a plain text editor or in KiCad itself in the GUI by clicking and typing in the boxes. Any project can be saved as a template and used later to start a new project with the same settings. 

It's important to me to make the transaction cost as small as possible for a KiCad design session. If I sit down and have to do a lot of tedious typing, it's more likely I'll make a mistake, or just skip the session all together. 

Also, if someone's going to pay me for five hours of design work, I don't want to work for an hour for free just trying to set up the project correctly.

For a start, I never want to have to edit these settings at the start of a project: 

- **Schematic Editor Options**
  - page size and company information
  - text sizes and line widths
  - where to find my libraries
- **Board Layout Editor Options**
  - my default set of trace widths
  - my default user grid
  - design rules 
    - minimum trace clearance
    - minimum drill sizes
  - minimal set of useful layers
  - which features to hide (such as values)

## Schematic Editor Settings

##### Page Size and Company Information

The schematic (.sch) and board layout (.kicad_pcb) files both can be set to any paper size so you print the file or save to a printable PDF. In both cases, typing `Wickerbox Electronics` on every single page is annoying, so I put it in my template, along with the license information.   

Templates can be just a blank project with empty schematic and layout pages, where the only benefit is the default settings, but I also wanted the schematic and layout to be printable to 8 1/2"x11" US Letter size pages and containing my name, the name of Wickerbox Electronics, and the license information. 
![Blank Schematic](/img/kicad/template-blank-schematic.png)

![Blank Company Information Box](/img/kicad/template-blank-company-info.png)

![Company Information Box](/img/kicad/template-company-info.png)

![Page Settings](/img/kicad/template-page-settings.png)

### Text and Graphics Sizes

This turns out to be more important for me in the board layout. I have certain sizes of lines on the Fab layer (so they come out well in the assembly diagrams) and other sizes for silk lines that will change based on the fabrication house capabilities. I might be able to get away with lines that are 3 mils thick at OSH Park, but I get best results with 4 mils and somewhere else might want 6 mils. I don't ever want to depend on remembering that when I'm in the middle of a design. 

![Schematic Editor Options](/img/kicad/template-schematic-options.png)

I usually use mm everywhere. 

![Layout Text and Drawings Options](/img/kicad/template-text-and-drawings.png)

KiCad's default Pad/Mask clearance is a huge 7 mils, which can cause shorts on the OSH Park service because the mask clearance and placement are 2.5 mils, but the minimum clearance between a trace and ground is only 6 mils. These are values that have worked for me: 

![Pad-Mask Clearance](/img/kicad/template-pads-mask-clearance.png)

### Library Information

I don't trust parts in other libraries, so I use my own libraries by default. KiCad looks for its own original libraries by default and will throw up this error message if you don't have any libraries of your own defined in the template: 

![Missing Default Libraries](/img/kicad/template-missing-default-libraries.png)

I don't want to have to click on Preferences > Component Libraries every single time and add the Wickerlib by hand. I put it in by default in the template. 

![Default Library](/img/kicad/template-default-library.png)

This lets me just hit `'a'` and immediately get wickerlib and (optionally) the cached libs of this schematic if there are any. 

![Wickerlib](/img/kicad/template-add-part.png)

### Design Rules

I sometimes need to create traces of certain impedance, so having those included means you don't have to go looking for them when you need them. 

![Design Rules Defaults](/img/kicad/template-design-rules-net-classes.png)

![Design Rules Globals](/img/kicad/template-design-rules-globals.png)

### Layer Setup

The template automatically hides the extra board layers I don't want to deal with, both in the layer setup screen and in the render tab under layout. I'm not concerned with mass fabrication at the moment, so I've hidden a lot of the fab and assembly-related layers.

Here's an image of the different layer setups. A shows the list with all the 32 possible inner layers made visible, along with all the assembly, fabrication, and notes layers. 

B shows just the two inner layers with all the extra assembly, fab, and notes layers. 

C shows my list of layers for a two layer board. Edge.Cuts has the board outline. The Fab layers will be my assembly diagram, and I use the Dwgs.User for fabrication notes. 

![Layer Setup](/img/kicad/layer-setup.png)

### Creating the Template

In the beginning, I used templates by opening KiCad and clicking File > New Project > New Project from Template. I'll explain how to do this here.

The way I do it now is completely scripted, but more information that over at <a href="#">KiFisher</a>.

Any kiCad project can be turned into a template by adding a 'meta' subfolder containing a 64x64-pixel image called logo.png and an HTML page called info.html. 

In this case, the 2-layer and 4-layer blank templates for Wickerbox Electronics were just empty projects with custom settings, but I've also created more complicated starter projects with existing components, a netlist, a board file containing a locked board outline, and so on. 

This is the `atmega328` project template. 

![Template Folder](/img/kicad/template-project-folder.png) 

As of KiCad 4.0.4, the default size and design rule settings are spread across the .pro, .kicad_pcb, and .sch files. My default templates included all three files.

KiCad builds the list of templates in its templates menu from the 64x64 icon and info.html file in the template project's meta folder. I couldn't figure out the formatting to get the titles to show up, so I put the title in the icon. 

![Icon](/img/kicad/template-icon.png)

This is what the `info.html` page looks like it if you open it by itself in the browser: 

![Info HTML](/img/kicad/template-html-info.png) 

### Using the Template

Before using a template, it's important to point KiCad at the template directory by updating KICAD_PTEMPLATES. This setting appears to be saved in the master kicad.pro configuration file, since I've only had to set it once. 

![Path Configuration](/img/kicad/template-path-config.png) 

Then, I start a new project from a template by opening KiCad and clicking on `File > New Project > New Project from Template`, or just hitting `Ctrl+T`.

There are two steps to the process. First, make a new folder with the filename of your project, and open that folder in KiCad. Once you do that, KiCad will show the list of templates. Yours are under the Portable Templates tab. 

![Selection with Icon](/img/kicad/template-selection.png) 

I find the template on the list and click OK, and KiCad will copy in all the project files (excluding the meta folder) into that folder. Then I just open up the project as normal, and since all my libraries are already listed correctly, Everything Just Works and I can get down to designing.

### Saving Default Settings

Making a template with just the design rules. 

Don't forget to save the settings by adding text, saving it, then deleting the text and saving it again! I didn't do that the ifrst time and PCBNew won't actually update the file if the only change was the settings, so you need some text to make the change stick. Then I decided I wanted to define the page layout for printing out, creating PDFs, or taking screenshots. I added company information and set the page to USLetter. I also hooked in the wickerlib project, so I don't have to go looking for my libraries. 

### Further Template Examples

Since I'd already hooked in the wickerlib project, I adapted an Arduino shield from __ and created my own Teensy and CHIP templates.    

Arduino, Teensy, and CHIP templates.

Finally, I decided to create my own Atemga328 breakout board, and to use a circuit I knew would work. I only created the schematic with the basics, since the idea would be to open the template and start adding and wiring in my additional circuitry for my custom board. There's no reason to recreate a proven circuit from scratch.

The next up will be a 1Bitsy template...

#### Extra

Before ever opening my CAD tool, I'll determine how many layers the board will be and if I'll be using a particular company (fab house) to manufacture the boards. I don't ever want to enter design rules by hand if I don't have to, since it's boring and also prone to human error, I'll create the new project from my template.
  
For example, a simple breakout board for a new chip might have two layers and I expect I'll order from OSH Park on their two layer service. That tells me what the design rules should be on my project. 

Since <a href="http://oshpark.com">OSH Park</a> is my fab house of choice, so I've created a project template that matches OSH Park's design rules and contains my most commonly used sizes of tracks and drills. The template also already has some of the Project Settings filled in for the schematic and PCB layout frames, so I don't have to type "Wickerbox Electronics" and click a lot every time I create a new project. 



