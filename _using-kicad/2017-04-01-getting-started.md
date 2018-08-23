---
layout: hardware
title: ROUGH Getting Started
description:
using-kicad: true
permalink: /hardware/automating-kicad/:title
---

Installing KiCad 4.0.4 from Ubuntu repos comes with Python scripting turned on. 

I haven't looked at [this site](https://kicad.mmccoo.com/kicad-scripting-table-of-contents/) but it looks amazing.

##### October 2016

Setting up KiCad, installed KiCad 4.0.4 stable. It came with Python scripting support already included. Easiest thing ever.

- Where to put my libraries
- Where to put my templates
- Where to put scripts and plugins

1. Adjust the Path Configuration. Where to put libraries, templates, scripts? Not in /usr/share/kicad, where they'll be potentially overwritten and they're not public anyway. Does Path COnfiguration box accept relative paths?

wickerlib itself contains templates, scripting, libraries, so it will be the top dir: /home/wicker/wickerlib, and the entire folder is a git repository. Adjusted the Path Configuration to match.

When I tried to redefine, I got an error message. This is because the default config (section 2.2 of <a href="http://docs.kicad-pcb.org/stable/en/pcbnew.html">the pcbnew doc</a>) is in kicad.pro in /usr/share/kicad/template/kicad.pro.

1. First thing to do is edit kicad.pro file... but it doesn't affect pcbnew and eeschema.

The real answer is to use a template. Never create a new project except from a template.

I fixed up the two Wickerbox basic 2-layer and 4-layer templates.

1. When making a new project,

- create git repo
- create folder
- start kicad
- file > new project from template
- place project in folder with same name
- open schematic
- adjust page settings
- start making schematic by adding parts from library

1. Add parts, making new ones if necessary.

The component has a symbol and all the part information for a specific part from a specific manufacturer. CAP-CER-22UF-X7R-0402-GRM1827391

1. When ready to Plot, settings are already present, including 'gerbers' subfolder

##### Installing KiCad 4

I'm using the KiCad new stable, version 4.0.1, which has all the new 2015 features.

<a href="http://kicad-pcb.org/download/">KiCad download information is here</a> for Mac, Windows, and Linux. 

I'm running Linux Mint 17.3, Rosa, which is based on Ubuntu 14.04 LTS. 

<hr>

##### My installation

Installing KiCad put the binary in `/usr/bin/kicad`. 

As part of the default install, KiCad automatically created `template` and `scripting` folders under `/usr/share/kicad/`, but it didn't immediately download and link local copies of all the symbols and footprints.

This is partly because the maintainers of the official KiCad libraries have set them up as Github repositories. The symbols have to be downloaded locally, at least for now, but the footprints can be added directly from Github while you're in the middle of designing the schematic or layout. 

Since I prefer to work offline, I had to figure out how to download and maintain lots of libraries on my local computer. To do that, first I had to figure out what KiCad thinks a library actually is. 

<hr>

##### What is a Parts Library?

**Components**

For components (symbols), KiCad considers a 'library' file to be the `libraryname.lib` file, and it also expects a `libraryname.dcm` file to be in the same folder. KiCad doesn't care if lots of different component libraries are all collected in the same folder. 

Each `libraryname.lib` file contains lots of symbols. For example, the official list of symbol libraries <a href="https://github.com/KiCad/kicad-library/tree/master/library">here</a> contains the official `atmel.lib` library file along with its corresponding `atmel.dcm` file in the same folder. When you include and open this `.lib` file in the Schematic Parts editor, it shows you a list of all the included parts so you can choose the one that best fits your schematic.

**Modules**

For modules (footprints), KiCad considers a 'library' file to be a folder that ends in `.pretty` that contains one or many module files that end in `.kicad_mod`. 

Unlike the component symbols, which are written text hidden inside one `.lib` text file, the new KiCad solution for footprints is to create a new and separate `.kicad_mod` file for each footprint. This way, editing or removing one doesn't affect any of the other files. 

The .pretty libraries are actually full git repositories themselves under the <a href="https://github.com/KiCad">KiCad</a> project on Github, so the repository for the `Capacitors_SMD.pretty` is <a href="https://github.com/KiCad/Capacitors_SMD.pretty">here</a>. 

The entire .pretty folder is itself the library that contains module files called `C_0402.kicad_mod`, `C_0603.kicad_mod`, `C_0603_HandSoldering`, and so on. The `.kicad_mod` module files are the different packages that you can choose when you associate a footprint with a symbol.

<hr>

##### What is a Parts Library?

**Components**

For components (symbols), KiCad considers a 'library' file to be the `libraryname.lib` file, and it also expects a `libraryname.dcm` file to be in the same folder. KiCad doesn't care if lots of different component libraries are all collected in the same folder. 

Each `libraryname.lib` file contains lots of symbols. For example, the official list of symbol libraries <a href="https://github.com/KiCad/kicad-library/tree/master/library">here</a> contains the official `atmel.lib` library file along with its corresponding `atmel.dcm` file in the same folder. When you include and open this `.lib` file in the Schematic Parts editor, it shows you a list of all the included parts so you can choose the one that best fits your schematic.

**Modules**

For modules (footprints), KiCad considers a 'library' file to be a folder that ends in `.pretty` that contains one or many module files that end in `.kicad_mod`. 

Unlike the component symbols, which are written text hidden inside one `.lib` text file, the new KiCad solution for footprints is to create a new and separate `.kicad_mod` file for each footprint. This way, editing or removing one doesn't affect any of the other files. 

The .pretty libraries are actually full git repositories themselves under the <a href="https://github.com/KiCad">KiCad</a> project on Github, so the repository for the `Capacitors_SMD.pretty` is <a href="https://github.com/KiCad/Capacitors_SMD.pretty">here</a>. 

The entire .pretty folder is itself the library that contains module files called `C_0402.kicad_mod`, `C_0603.kicad_mod`, `C_0603_HandSoldering`, and so on. The `.kicad_mod` module files are the different packages that you can choose when you associate a footprint with a symbol.

<hr>

##### Setting up my Library Folders

Once I knew what KiCad wanted a library to look like, I had to figure out how the libraries are arranged on my computer. I have basically three sources of KiCad library files: 

1. The official KiCad libraries
2. My wickerlib libraries
3. Other libraries from random people

Every folder in this list contains one of those three possible sources: 

{% highlight bash %}
# official libraries
~/proj/kicad/library-repos/symbols/     
~/proj/kicad/library-repos/footprints   
~/proj/kicad/library-repos/templates   

# wicker libraries
~/proj/kicad/wickerlib-kicad/symbols/   
~/proj/kicad/wickerlib-kicad/footprints
~/proj/kicad/wickerlib-kicad/templates  

# other random libraries
~/proj/kicad/example_board_lib1/       
~/proj/kicad/example_board_lib2/      
~/proj/kicad/and-so-on-lib/          
{% endhighlight %}

**Official KiCad Libraries**

Other people leave the KiCad repositories on Github but I like to work offline so I created a folder called `~/proj/kicad/library-repos/` and followed the instructions from the <a href="https://github.com/KiCad/kicad-source-mirror/blob/master/scripts/library-repos-install.sh">libgrary-repos-install script here</a> to copy all of the KiCad footprint libraries to a directory called `~/kicad_sources`. 

Then I moved all the `.pretty` folders in that directory to `~/proj/kicad/library-repos/footprints/`.

To get the symbols, I cloned the <a href="https://github.com/KiCad/kicad-library">kicad-library</a> github repo. I moved and renamed the `library` folder to `~/proj/kicad/library-repos/symbols` and the `template` folder to `~/proj/kicad/library-repos/templates`. 

**My wickerlib Libraries**

Because I'm leaving the official KiCad libraries as read-only references, I'll either use them as-is or I'll copy them into my own `wickerlib` set of libraries before editing. That way, there's no confusion about what's proven and what's not.

The `~/proj/kicad/wickerlib-kicad` folder contains a public, forkable git repository called <a href="https://github.com/wicker/wickerlib-kicad">wickerlib-kicad</a> that's where I keep my component (symbols), module (packages/footprints), and project templates. 

This git repository looks something like this:

{% highlight bash %}
footprints/esp8266.pretty/esp01.kicad_mod
footprints/esp8266.pretty/esp12e.kicad_mod
footprints/rf24.pretty/nRF24.kicad_mod
symbols/rf24.dcm
symbols/rf24.lib
symbols/wicker-crystal.dcm
symbols/wicker-crystal.lib
{% endhighlight %}

**Other project libraries**

As I download other projects or collaborate with other folks, I'll keep the libraries for these projects more or less in the same root `~/proj/kicad` folders.

<hr>

The only trick with setting up my folders this way is how to tell KiCad where to find them.

For the symbols, I edited the `LibDir` variable under `[eeschema]` in each  KiCad Project file. 

Since I use a template to create new projects, I opened the .pro file of my template project in a text editor and set all the library-related variables to match my folders.

{% highlight bash %}
[eeschema]
version=1
LibDir=/home/wicker/proj/kicad/
[eeschema/libraries]
LibName1=kicad-library/power
LibName2=kicad-library/device
LibName3=kicad-library/transistors
LibName4=kicad-library/conn
LibName5=kicad-library/linear
LibName6=kicad-library/regul
LibName7=kicad-library/74xx
LibName8=kicad-library/cmos4000
LibName9=kicad-library/adc-dac
LibName10=kicad-library/memory
LibName11=kicad-library/xilinx
LibName12=kicad-library/microcontrollers
LibName13=kicad-library/dsp
LibName14=kicad-library/microchip
LibName15=kicad-library/analog_switches
LibName16=kicad-library/motorola
LibName17=kicad-library/texas
LibName18=kicad-library/intel
LibName19=kicad-library/audio
LibName20=kicad-library/interface
LibName21=kicad-library/digital-audio
LibName22=kicad-library/philips
LibName23=kicad-library/display
LibName24=kicad-library/cypress
LibName25=kicad-library/siliconi
LibName26=kicad-library/opto
LibName27=kicad-library/atmel
LibName28=kicad-library/contrib
LibName29=kicad-library/valves
LibName30=wickerlib-kicad/symbols/wicker-dds
LibName31=wickerlib-kicad/symbols/wicker-crystal
LibName32=wickerlib-kicad/symbols/wicker-test
{% endhighlight %}

For the footprints, KiCad uses the list of libraries in `~/.config/kicad/fp-lib-table` along with the system variable `KISYSMOD`, so I added a line in my `~/.bashrc` to set that system variable:

{% highlight bash %}
export KISYSMOD="/home/wicker/kicad_sources/library-repos/"
{% endhighlight %}

First, I cloned my own <a href="http://github.com/wicker/wickerlib-kicad">wicker/wickerlib-kicad</a> git repo. 

For the official libraries, I had to get the files from Github before I could move them into my 'official' `kicad-library` folders.

To get the symbols and templates, I cloned <a href="https://github.com/KiCad/kicad-library">KiCad/kicad-library</a>, and copied the `library` folder into `symbols` and the `template` folder into `templates`. In the future, I could pull updates and rsync them over if I wanted, but for now I'm not worried about it. 

To get the footprints, I copied the .pretty libs into `kicad-library/footprints` by following the instructions in the <a href="https://github.com/KiCad/kicad-source-mirror/blob/master/scripts/library-repos-install.sh">library-repos-install.sh</a> script. 

I ran `./library-repos-install.sh --install-or-update` and ended up with all of the .pretty repos in a folder in `/home/wicker/kicad_sources/library-repos/kicad-library` so I was able to copy just what I needed into `~/proj/kicad/kicad-library/footprints`. 

Finally, to link everything up, I had to edit the fp-lib-table file.

KiCad uses the Library Tables file in each project as part of the PCB Footprint Wizard so it can find the .pretty module (footprint) libraries. I always use the Wizard when I'm starting a new layout in PCBNew, so I copied the Library Table file from `~/proj/kicad/library-repos` `template/fp-lib-table.for-pretty` into KiCad's config file at `~/.config/kicad/fp-lib-table`. 

KiCad needs `KISYSMOD` to point to the library repos. In a standard installation, it points at `/usr/local/modules`. 

Finally, the last step was to edit `/etc/profile.d/kicad.sh` to set `KISYSMOD` to `~/proj/kicad/library-repos`

Now KiCad wil look for `*.pretty` footprint files in `~/proj/kicad/library-repos`. The burden of maintaining and checking for library updates falls on me, but that's fine. 

<hr>

##### Working Folders

Now that KiCad is installed and the libraries are available, the next step is figuring out how to organize each project folder. First, here's how I typically organize the working directories on my Linux computer:

{% highlight bash %}
~/proj/adafruit/random-adafruit-library
~/proj/desertlizard/lizardware
~/proj/eagle/wickerlib-eagle
~/proj/kicad
~/proj/kicad/library-repos
~/proj/kicad/wickerlib-kicad
~/proj/wicker/project1
~/proj/wicker/project2
~/proj/wicker/wicker.github.io
~/scratch
~/tools/arduino-1.6.5
~/tools/eagle-6.6.0
{% endhighlight %}

All of my current hardware and software projects are captured in git repositories in my ~/proj directory. I'll often clone github repos from places like Sparkfun or Adafruit into their own subfolders so I can keep track of where I got stuff.

The scratch folder can be deleted at any time, and nothing seriously important stays in there. It's a temporary working directory. When it gets too full, it gets deleted.


I install my tools in `~/tools` when they're not in `/usr/local/bin`. Certainly, I keep the source of the tools in `~/tools` for future reference.  

The `wickerlib-eagle` and `wickerlib-kicad` folders are my own repositories of footprints for Eagle and KiCad. I'm excited by the KiCad .pretty libs being on Github because it means I can start contributing proven footprints back to the main libraries!

<hr>

##### Anatomy of a KiCad Github Project Repo

Let's say `~/proj/wicker/project1` is where I want to create a KiCad project, and I want to upload it to Github for version control and safekeeping. This is how I generally organize the files in my KiCad project repositories: 

{% highlight bash %}
.gitignore  # don't track kicad cruft 
README      # overall project documentation!
LICENSE     # usually the CERN OHL v1.2
.pro        # KiCad project file
.sch        # EESchema schematic
-cache.lib  # local cached copy of schematic symbols
.kicad_pcb  # PCBNew layout 
.net        # netlist
.xml        # bill of materials 
.dxf        # mechanical outline drawings
symbols/ 
    .lib    # info to draw the symbol
    .dcm    # symbol documentation info
footprints/
    .pretty # library of .kicad_mod parts
gerbers/
    name-Edge.Cuts.gm1  # board outline
    name-F.Cu.gtl       # top copper
    name-F.Mask.gts     # top mask
    name-F.SilkS.gto    # top silk
    name-B.Cu.gbl       # bottom copper
    name-B.Mask.gbs     # bottom mask
    name-B.SilkS.gbo    # bottom silk
    name-In1.Cu.g2      # internal plane 1 (if 4-layer)
    name-In2.Cu.g3      # internal plane 2 (if 4-layer)
    name.drl            # drill file
print/
    sch.pdf # pdf of the schematic
    pcb.pdf # pdf of the PCB layout
{% endhighlight %}

The .gitignore file is incredibly simple:

{% highlight bash %}
# Backup files
_autosave*
*.bak
*.kicad_pcb-bak
{% endhighlight %}

To simplify keeping track of my library parts, I've decided to avoid the old KiCad .mod files entirely. If there's an old footprint that appears to be exactly what I need, I'd rather take the time to make a .pretty and share that instead.  

<hr>

##### Distributing KiCad Files

I'm a little worried about how to distribute KiCad project git repos when I'm internally referencing .pretty repos and library files that aren't local. I know we have -cache.lib files, but what about .pretty? I haven't actually reached a satisfactory solution for this yet. 

<hr>
