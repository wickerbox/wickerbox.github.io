---
layout: hardware
title: ROUGH Footprint Library
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

Schematics are functional descriptions of circuits that don't have anything to do with the board layout. In a lot of companies, the people who actually lay out the board aren't the same people who design the schematic. 

When I started, I hated that Eagle forced me to pick a final footprint when I was still just trying to figure out how the schematic worked. It didn't feel natural in my design process. 

KiCad keeps symbols and footprints in separate libraries and doesn't force you to associated them until you want to. This was a big plus for me and it made the switch to KiCad a little easier.

Initially, I kept a pile of symbol libraries and a pile of footprint libraries. When the default KiCad libraries didn't have what I needed, I created new symbols and footprints for my own libraries. Everything was scattered around, which made it hard to keep track of.

Most of my libraries only had the variables for Name, Value, Footprint, and Datasheet.

Eventually, I had enough parts floating around my workroom that I needed some way to keep track of them, so I could buy in bulk and then use parts I already had in stock. 

The easiest way to keep track of interchangeable parts is to create a company-specific part numbering system and create symbols based on that numbering system. The end result here is to create a schematic and select symbols that have a company part number. They'll come immediately with information about the associated part, including footprint. 

Rheingold Heavy has an article about the making <a href="https://rheingoldheavy.com/kicad-bom-management-part-1-detailed-components/">detailed components</a> that will help generate KiCad Bills of Material (BOMs). 

I stopped thinking about symbols and footprints as two equal halves of a whole functional description of a part. Instead, I started seeing the symbols as most of the description. 

I have a company part number, a symbolic picture on the schematic, and an associated footprint. I realized that the symbolic picture (component) is most of the data.

A company part number could be associated with multiple symbolic pictures. In my bill of material system, all of these are valid at the same time: 

|Inventory Number|Symbol|Footprint|
|----------------|------|---------|
|0001|Symbol configuration #1|8DIP|
|0002|Symbol configuration #1|8SOIC|
|0001|Symbol with hidden pins|8DIP|

I thought back to my first electrical engineering job for ideas on what worked best. Combined with the Rheingold Heavy article suggestions, I came up with this list of additional 

The next step was to inventory my workroom. That took ... a while. I made up a spreadsheet with all of my component parts. Another name for inventory number is a SKU, or stock keeping unit.  

- Reference
- Value
- KiCad Footprint
- Datasheet
- WBox_SKU
- Description
- Package
- MF_Name
- MF_PN
- S1_Name
- S1_PN

Armed with this list, I did some reading from the Rheingold Heavy article and a couple others that were linked, including Spark's <a href="http://www.proto2prod.com/proto2prod/2015/3/11/creating-and-optimizing-a-bill-of-materials-1">Creating and Optimizing a Bill of Materials</a> and Bunnie Huang's <a href="http://www.bunniestudios.com/blog/?p=2776">The Factory Floor</a>.

I decided to use all of the above variables in my library parts in KiCad, but also to add a second source and part number. I was also going to look into how KiCad generates the position and orientation, and make sure my ultimate exported BOM included those values:  

- S2_Name
- S2_PN
- Position
- Orientation

Luckily, at some point if I'm ever ordering giant production runs, KiCad files are all text editable so I can go back and use sed to batch-insert other variables. For now, for prototype runs, the variables on this list will save me a lot of time and struggle at the moment when I need to make an order. 
  
### Add parts to the library

My parts would all be entirely described in a single symbol library (wickerlib.lib) and a single footprints library (wickerlib.pretty) because KiCad has a decent search function once you've opened a particular library. This way, I can also just add parts to the libraries and never have to worry about sorting, categorizing, or placing parts in the correct library.

I created a Python script that walked through a .csv version of my inventory. Every SKU should have at least one entry, though it may have multiple entries because there may be more than one symbol attached to that stock item. Each stock item necessarily only has one footprint. Components with different packages have different stock numbers. 

### Properties and Where to Find Them

Properties both in the symbol and the main KiCad schematic editor.

- Do schematic editor template options follow the schematic or are they attached to the KiCad program itself? Where are they stored?

Ideally, you would make up the list of properties you want them to have. That will be the first four plus some set of others.

### Setting up Schematic Editor Properties to Match What You Want

In the schematic editor, use `e` to open a component's properties. There should be the first four default fields of Reference, Value, Footprint, and Datasheet. 

<img src="/img/toolbox/component-properties-top4.png">

To add properties to this list, you have to add them in the KiCad Schematic Editor under Preferences > Schematic Editor Options, on the Template Field Names tab. 

<img src="/img/toolbox/template-field-names.png">

After you've done that, if you go back to the open a component's properties in the schematic, you'll see the whole list.

<img src="/img/toolbox/component-properties-all.png">

Adding a hundred components would suck, but I have a spreadsheet with all these column categories so I'm going to try scripting and just adding lots of entries to the raw symbol text files. 

### Editing Symbols by Hand

This is an example component entry in the DCM file, which holds descriptions, keywords, aliases, and reference links for library symbols.

{% highlight bash %}
#
$CMP ATTINY261V-20SOIC
D  IC MCU 8BIT 8KB FLASH 20SOIC 
K AVR 8bit Microcontroller tinyAVR
F http://www.atmel.com/...datasheet.pdf
$ENDCMP
{% endhighlight %}

This is an example component entry in the LIB file, which is linked to the item of the same name in the DCM. The fields F0 through F10 contain the four default field values defined in plus the fields 

{% highlight bash %}
#
# ATTINY261V-20SOIC
#
DEF ATTINY261V-20SOIC IC 0 40 Y Y 1 F N
F0 "IC" -850 950 50 H V C CNN
F1 "ATTINY261V-20SOIC" 600 -950 50 H V C CNN
F2 "" -950 850 50 H V C CIN
F3 "http://www...datasheet.pdf" 50 1500 50 H I C CNN
F4 "Digikey" -350 1450 60 H I C CNN "S1_Name"
F5 "0002" -350 1400 60 H I C CNN "Wbox_SKU"
F6 "IC MCU 8BIT" 300 2050 60 H I C CNN "Description"
F7 "20SOIC" -300 1650 60 H I C CNN "Package"
F8 "Atmel" -350 1750 60 H I C CNN "MF_Name"
F9 "ATTINY861V-10SU" 250 1750 60 H I C CNN "MF_PN"
F10 "ATTINY..ND" 400 1850 60 H I C CNN "S1_PN"
DRAW
ENDDRAW
ENDDEF
{% endhighlight %}

- F0 looks like Reference
- F1 looks like Value
- F2 looks like 
- F3 looks like the datasheet link

The other field entries occur out of order and in no particular order. 

You can only edit the DCM values by opening the part in the Part Library Editor and 'Edit Component Properties' using the ABC/gear symbol. 

You can use the black T symbol to 'Add and Edit fields and edit field properties' manually, but that takes a lot of time and effort.

<img src="/img/toolbox/editor.png">

The DCM file has nothing to do with the values in LIB. The Documentation File Name entry there is only reflected in the DCM. The only reason to use the DCM is because the desciprtion is used to search, which is incredibly useful to find the parts in KiCad's search. The documentation link there doesn't go anywhere else, and F3 is the datasheet link from in the schematic editor.  

<img src="/img/toolbox/dcm-source.png">

You can add any fields you want to the actual physical LIB entry, and KiCad will add them whether or not the schematic template contains the list of fields. It also includes any additional ones from KiCad's schematic editor options.  

##### Questions

You can't determine which category based on the F-number; F0, F1, etc. You have to determine if a line is a field entry and read the last element in the line to determine the name of the category. 

- What's the difference between F in DCM and Datasheet entry in LIB? F in DCM has nothing to do with anything, it just sits in the documentation file. No effect on datasheet entry in LIB. I'm going to exclusively bother with the datasheet entry in LIB and only use the DCM entries for keywords for searching. 

- What happens when you manually add field entries that are duplicate F-numbers? Doesn't seem to matter.
- What happens when you manually add field entries out of order in text and then open that entry in the library editor? F1, F2, F8, F3, F7, F5, F4, F6?  Doesn't seem to matter. 


I entered them all like this, with all additional entries as F5: 

{% highlight bash %}
#
# ATTINY261V-20SOIC
#
DEF ATTINY261V-20SOIC IC 0 40 Y Y 1 F N
F0 "IC" -850 950 50 H V C CNN
F1 "ATTINY261V-20SOIC" 600 -950 50 H V C CNN
F2 "" -950 850 50 H V C CIN
F3 "http://www.agoof.html61-attiny461-attiny861_datasheet.pdf" 50 1500 50 H I C CNN
F5 "Digikey" -350 1450 60 H I C CNN "S1_Name"
F5 "0002" -350 1400 60 H I C CNN "Wbox_SKU"
F5 "IC MCU 8BIT 8KB FLASH 20SOIC " 300 2050 60 H I C CNN "Description"
F5 "20SOIC" -300 1650 60 H I C CNN "Package"
F5 "Atmel" -350 1750 60 H I C CNN "MF_Name"
F5 "ATTINY861V-10SU" 250 1750 60 H I C CNN "MF_PN"
F5 "ATTINY861V-10SU-ND" 400 1850 60 H I C CNN "S1_PN"
{% endhighlight %}

In the schematic file, they get placed in order based on the Template FIeld Names order: 

{% highlight bash %}
$Comp
L ATTINY261V-20SOIC IC?
U 1 1 56F8432A
P 9000 2200
F 0 "IC?" H 8150 3150 50  0000 C CNN
F 1 "ATTINY261V-20SOIC" H 9600 1250 50  0000 C CNN
F 2 "" H 8050 3050 50  0000 C CIN
F 3 "http://www.agoof.html61-attiny461-attiny861_datasheet.pdf" H 9050 3700 50  0001 C CNN
F 4 "Digikey" H 8650 3650 60  0001 C CNN "S1_Name"
F 5 "0002" H 8650 3600 60  0001 C CNN "Wbox_SKU"
F 6 "20SOIC" H 8700 3850 60  0001 C CNN "Package"
F 7 "Atmel" H 8650 3950 60  0001 C CNN "MF_Name"
F 8 "ATTINY861V-10SU" H 9250 3950 60  0001 C CNN "MF_PN"
F 9 "ATTINY861V-10SU-ND" H 9400 4050 60  0001 C CNN "S1_PN"
F 10 "IC MCU 8BIT 8KB FLASH 20SOIC " H 9300 4250 60  0001 C CNN "Description"
  1    9000 2200
  1    0    0    -1  
$EndComp
{% endhighlight %}

- What if the list of field categories in the part doesn't match the list that's in KiCad schematic view? I added an extra field called Extrafield. The library part doesn't get updated with this, but the .sch file does. Cache lib does not. 

Adding extra fields in the schematic editor only touches the .sch file. 

{% highlight bash %}
$Comp
L ATTINY261V-20SOIC IC?
U 1 1 56F84468
P 8850 2175
F 0 "IC?" H 8000 3125 50  0000 C CNN
F 1 "ATTINY261V-20SOIC" H 9450 1225 50  0000 C CNN
F 2 "" H 7900 3025 50  0000 C CIN
F 3 "http://www.agoof.html61-attiny461-attiny861_datasheet.pdf" H 8900 3675 50  0001 C CNN
F 4 "0002" H 8500 3575 60  0001 C CNN "Wbox_SKU"
F 5 "20SOIC" H 8550 3825 60  0001 C CNN "Package"
F 6 "Atmel" H 8500 3925 60  0001 C CNN "MF_Name"
F 7 "ATTINY861V-10SU" H 9100 3925 60  0001 C CNN "MF_PN"
F 8 "Digikey" H 8500 3625 60  0001 C CNN "S1_Name"
F 9 "ATTINY861V-10SU-ND" H 9250 4025 60  0001 C CNN "S1_PN"
F 10 "IC MCU 8BIT 8KB FLASH 20SOIC " H 9150 4225 60  0001 C CNN "Description"
F 11 "Foo" H 8850 2175 60  0001 C CNN "Extrafield"
  1    8850 2175
  1    0    0    -1  
$EndComp
{% endhighlight %}

- What if the schematic editor has less information than the library? What if I don't want to propagate Wbox_SKU values out into the world? 

It gets added automatically to the component properties!

<img src="/img/toolbox/test-nosku.png">

<img src="/img/toolbox/test-nosku-resultproperties.png">

WBox_SKU shows up in the .sch file:

{% highlight bash %}
L ATTINY261V-20SOIC IC?
U 1 1 56F84552
P 8125 1875
F 0 "IC?" H 7275 2825 50  0000 C CNN
F 1 "ATTINY261V-20SOIC" H 8725 925 50  0000 C CNN
F 2 "" H 7175 2725 50  0000 C CIN
F 3 "http://www.agoof.html61-attiny461-attiny861_datasheet.pdf" H 8175 3375 50  0001 C CNN
F 4 "Digikey" H 7775 3325 60  0001 C CNN "S1_Name"
F 5 "0002" H 7775 3275 60  0001 C CNN "Wbox_SKU"
F 6 "20SOIC" H 7825 3525 60  0001 C CNN "Package"
F 7 "Atmel" H 7775 3625 60  0001 C CNN "MF_Name"
F 8 "ATTINY861V-10SU" H 8375 3625 60  0001 C CNN "MF_PN"
F 9 "ATTINY861V-10SU-ND" H 8525 3725 60  0001 C CNN "S1_PN"
F 10 "IC MCU 8BIT 8KB FLASH 20SOIC " H 8425 3925 60  0001 C CNN "Description"
{% endhighlight %}

- What if schematic and library explicitly disagree?

Library overrides the schematic editor. I set the value of MF_PN to be `TESTSOURCE` and it didn't show up in the .sch or the -cache.lib. The value in wickerlib.lib entirely overrode it.

- What if F0-F3 values are named wrong? 

- What information is kept in the template? 

### Next

- Update all of the designs released through Wickerbox to depend on those libraries, so to use them all anybody has to do is download the KiCad project and the latest wickerlib files.

- With all that in place, I created a Python script that created a BOM. There are a couple of different BOM formats to output, but for now just the simple Github BOM.

### Thoughts

Somebody wants a design. I work out of Wickerlib to start, adding parts and adding SKU numbers even if I don't have any in stock. I update my inventory and I sync my library.

When I'm ready to create gerbers, I create a BOM based on whichever set of info I want. 

I can create a new library and rename everything and clean it up for those other people. 

Or I can just save the .sch, .pro, .kicad_pcb, .net, -bom.csv and call it good.

# Older

Adding a component is easy. Editing a component is confusing because it's not clear what and where the editing is happening, not is it clear what exactly should be loaded into the library editor. 

First, before using the Schematics Parts Editor or Footprint Editor to edit libraries, I had to remember some things about KiCad and libraries. figure out what KiCad thinks a library is. Now that I know where the libraries are, I'm ready to add and edit them. This works as long as I'm very clear about what I'm trying to do. 

First off, when I need to edit or add a part, I open my schematic in EESchema and go to `Tools > Library Editor`.

When it opens, the editor will say `Part Library Editor: no library selected` in the title area at the top of the program. 

<img src="/img/kicad/nolibrary.png">

What I do next depends on whether I'm working with an existing or new library. I can: 

1. Edit an existing part in an existing library.
1. Add a new part to an existing library.
1. Add a new part to a new library.

**Existing Library**

To edit or add a component to an existing library, I first go to `File > Current Library` and select a library from the list. If I'm using a standard KiCad library, the library will open but the title bar will now say `Parts Library Editor:` with the location and name of the repo, along with `[Read Only]`. 

<img src="/img/kicad/libraryreadonly.png">

I actually think stopping me from writing over the existing official KiCad libraries is a good thing. I can open the components and copy them into my own wickerlib libraries, but I can't replace them with unproven component information. 

If I wanted to edit an existing component from this `atmel.lib` library, I would have to create a new library and either a) copy the symbol over, or b) reproduce it from scratch. 

The important thing to know here is that the `File` menu only deals with **libraries** and it's the little red op amp menu symbols that actually save, upload, or download individual **symbols**. I often want to hit `Ctrl+S` and save the symbol, but that's going to be frustrating because KiCad thinks I want to save the **library**. Instead, I have to choose the correct **symbol** icon.

<img src="/img/kicad/symbolicons.png" style="max-width: 158px;float:right;">
There are four of them:

1. Add a new component.
2. Load an existing component to edit from the current library.
3. Create a new component from the current component.
4. Update the current component in current library.

Since I'm in an existing, read-only library, I can either create a new component, but not save it here (option #1) or load an existing component from this library and choose to create a new component from the current one (option #2, then option #3). 

In both cases, I end up with a component in the window that I'm ready to save. 

If I want to edit a component in a library that's not read-only, I'll choose the second option and select the component. Then, depending on how major the changes to the symbol are, I can either use the third option to create a new component alongside the existing one, or I can overwrite the existing component. 

Usually, if the changes are minor or desired to modify a current schematic, I'll overwrite.

Otherwise, if the changes are significant and might affect previous schematics, I'll create a new component to be safe. 

Because the library already exists, I can close the Parts Editor and all I have to do back in the EESchema is hit `F3` to redraw the schematic to redraw any existing components. 

If I added a new component, it will automatically be available in my library so I just have to hit `a` to add and find it. 

**New Library**

If I'm adding a brand new kind of part and I don't have a suitable library for it, I have to open the Library Editor and create a new component. I usually just add an outline of something and then go to `Export Component` in the menu bar and save it with the same naming scheme with my other custom libraries.

In this case, I chose to call it `wicker-test.lib` and to save it in my `~/proj/kicad/wickerlib-kicad/symbols/` directory.

Now that the library exists, I have to make it available for use by going to `Preferences > Component Libraries` and using the top `Add` button to `Add a new library after the selected library and load it`.

I navigate to the right directory and select the `wicker-test.lib` file. When I scroll down to the bottom of the list, my new library will be there.

Now the library exists, so I can go to `File > Current Library` and select it from the list. The title bar at the top will now say `Part Library Editor` with the name of the library.

Any further work I do is now the same as with an existing library. The componentI loaded is already present, so all I have to do is edit and `update current component in current library.`

<hr>

##### Using the Schematic Parts Editor

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

##### Footprint Editor

Anyway, back to the Footprint Editor. If I need to add a footprint, the first thing to do is open up the editor. I can get to it from EESchema or from PCBNew, and I'll edit footprints from either place. 

<img src="/img/kicad/eeschematop.png">

Just like the schematic editor, it says no active library; that's OK, because I'm going to select one. I'm not creating anything, just browsing, so it doesn't matter if my libraries are read-only.

Remember, the `File` menu opens and saves the `.pretty` library itself. The green-padded footprint icons in the top bar open, copy, and work on the `.kicad_mod` footprint files themselves.

<img src="/img/kicad/footprinteditor-top.png">

I basically just open the Footprint Library, go to `File > Set Active Library` and select the library I'm thinking about editing. 



<hr>

##### Creating Footprints

Most of the hotkeys are the same. The template should take care of whether it's mm or inches. 

Click and dragging to select seems to work for moving, though it doesn't grab.

Holding shift or control while clicking and dragging makes a copy of the whole group.

Holding shift and control while clicking and dragging deletes everything that was selected.

I use 'd' for delete, because it lets me move with the right hand on the mousepad and use the left hand. All my hotkeys should be like this.

Would like to just hit enter from anywhere in the Footprint Editor Footprint Text Editor window.

`w` for next track width
`shift+w` for previous track width
`i` existing select copper track
`v` toggles between top and bottom copper layers

# Libraries

There are component libraries (containing part information and the schematic symbol in one .dcm and one .lib file per library) and module libraries (containing the footprint in a .kicad_mod file in the .pretty library folder). 

### Component Library Parts

I create a new component part for each part number so that the footprint is already associated and I can generate the bill of materials as soon I've finished the schematic. This lets me make sure the part is in stock somewhere before I start my design. 

![Component with Symbol](../images/libraries-component.png)

In the .dcm file, I just have the description and nothing else. There are other possible fields but I don't use them, including them instead in the .lib file. Here's the example entry for the 10uF capacitor above: 

```
#
$CMP CAP-CER-10UF-25V-X7R-1210
D CAP CER 10UF 25V X7R 1210
$ENDCMP
```

In the .lib file, the corresponding component entry has a bunch of additional fields. The commented line at the top and the DEF line match the $CMP name in the .dcm file. Fields 0 through 3 are required fields:

- F0 Reference Designator
- F1 Name
- F2 Footprint
- F3 Datasheet

The others are extra fields that I've added. I've also used Package and Verified in the past, but ended up not ever using them for anything.

```
#
# CAP-CER-10UF-25V-X7R-1210
#
DEF CAP-CER-10UF-25V-X7R-1210 C 0 40 N N 1 F N
F0 "C" 100 50 50 H V L CNN
F1 "CAP-CER-10UF-25V-X7R-1210" 100 -50 50 H V L CNN
F2 "Wickerlib:RLC-1210-SMD" 0 -350 50 H I C CIN
F3 "http://www.yuden.co.jp/productdata/catalog/en/mlcc_all_e.pdf" 0 0 5 H I C CNN
F4 "Taiyo Yuden" 0 -350 50 H I C CIN "MF_Name"
F5 "TMK325B7106KN-TR" 0 -350 50 H I C CIN "MF_PN"
F6 "Digikey" 0 -350 50 H I C CIN "S1_Name"
F7 "587-2599-1-ND" 0 -350 50 H I C CIN "S1_PN"
F8 "CAP CER 10UF 25V X7R 1210" 0 -350 50 H I C CIN "Description"
DRAW
P 2 0 1 13 -60 -20 60 -20 N
P 2 0 1 12 -60 20 60 20 N
X ~ 1 0 100 75 D 40 40 1 1 P
X ~ 2 0 -100 80 U 40 40 1 1 P
ENDDRAW
ENDDEF
``` 

To create a new part, first I find the part in the vendor website (such as Digikey). 

Then I open the library editor and open a part that has a similar or identical schematic symbol. This is particularly easy for capacitors, etc. I can add that part to the schematic and click Ctrl+E to open the part in the library editor. 

The other fields are present but grayed out because I've hidden them. 

![Edit the Component Fields](../images/libraries-editcmp.png)

First, I click the teal-colored component name with the dashes, and I change the name. It needs to follow the trend of COMPONENT-SPECIFIC-VARIABLES-PACKAGE-PARTNUMBER, though part number is often ignored for the moment. Ideally all the parts will be converted to the full name. 

Then I save the part, and KiCad will save the component into a new part, creating a new $CMP entry in both the .lib and the .dcm files. The part still has the previous part's information in the fields, so that's what I have to adjust next. 

Now I click the gear icon in the top menu and change the description to match the new name. This updates the 'D' field in the .dcm file. I usually copy this to the clipboard for the next step...

![Edit the Description](../images/libraries-editdesc.png)

Finally, starting with the full description variable, I click 'E' on each of the gray hidden fields and copy/paste the part information. Once that's done, I save the component and go back to the schematic editor to add it. Done.

### Footprints

Footprint files are called .kicad_mod files and they're kept in a folder that has the Libraryname.pretty. In this case, I use Wickerlib.pretty. I've created footprints but I've also adapted them from the main libraries, so I've added a comment header that looks something like this:

```
# KiCad Footprint 
# Originally from the KiCad Official Libraries
#   http://github.com/kicad/
# Edited by Jenner for Wickerlib
#   http://github.com/wickerbox/wickerlib
# This library file is provided under the GPLv3
#   https://www.gnu.org/licenses/gpl-3.0.html
# The footprint may not be correct! It is the end
# user's responsibility to verify the package.
```

It contains any history information about who created the package, then notes about whether I've modified it or not, a disclaimer about it not being verified, and the license information.

The footprint naming scheme is still haphazard but generally goes left to right from most generic feature to least, and it includes the part number if the part has a unique footprint. 

To create a new footprint, I open the library I want to save it in and use the New Footprint icon. I create the footprint on the copper, mask, paste, and silk layers, but ignore any silk text for nwo. 

I include assembly diagram information on the footprint so I can create the assembly diagram on the F.Fab and B.Fab layers with the same click as when I generate the rest of my gerbers. To that end, I place the reference designator and value items on the F.Fab layer. I make the value invisible, and I move the reference designator to the center of the footprint.

The KiCad Library Convention suggests a courtyard around the part at certain distances, depending on the part, so I create that and then place a copy of the box on the F.Fab layer as well. 

If I stopped now, I wouldn't have any silk text on the board, but I usually do like to have reference designators so I add a text item labeled %R. This will inherit the reference designator value, as shown below. The teal item is the silk item; the yellow C14 text is the actual reference designator on the F.Fab layer, and the 10uF 25V value is on the F.Fab layer but grayed out because it's invisible. It won't show up on the assembly diagram.

![Footprint Layers](../images/libraries-footprint.png)

The fab layer will also include any polarity markings or other assembly information, but a bidirectional capacitor is quite possibly the most simple footprint ever.

![Fab Layer Only](../images/libraries-fabonly.png)


