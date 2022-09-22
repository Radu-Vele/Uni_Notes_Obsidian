---
tags: [Notebooks/Digilent]
title: "Course Notes 10.05.2022 \U0001F34A"
created: '2022-05-10T13:29:56.397Z'
modified: '2022-05-17T12:30:28.308Z'
---

# Course Notes 10.05.2022 :tangerine:

## Homework feedback 
- in last notes file

Petalinux uses `Yocto` -> Creates a custom embedded 
distribution of linux

# Yocto

`documentation: Layers, Recipes, Bitbake petalinux-related`

> Yocto is a tool that puts together uboot, kernel, customizable packages (+nano, vim, git etc.) (Usually for embedded & IoT)

- I can configure my Linux distribution using yocto commands

- open-source

- any uP or uC that works with linux it s useful (ARM mostly)

- pulls from official repos for uBoot, kernel, packafes

-> images | linux

- we can create packages and use a package manager + custom made apps we have

Useful packeges to create
- apt: useful for installing stuff.

### More on yocto -- see yocto architecture workflow diagram
- can create more patches, kernel configurations (that could be given as inputs to the buld system)
- pre-configured: Machine BSP config (e.g. for Xilinx there is a special bsp.) , Metadata, Policy config.
- pre-configured settings could be customized using `$ petalinux config`
 
- **github** xilinx has repos for linux kernel / uboot

- bitbaker files (.bb) contain valuable info (*look it up* :triangular_flag_on_post:)

- packages work somehow like .exe installers -ish

- QA tests: could be defined by us (not so facilitated by petalinux tho). 

---

### Yocto ***LAYERS***
- support collaboration & customization

> Layer = repository that contains instruction for OpenEmbedded System (the buikd system)

- \+ ability to override previous instructions (customization)
- \+ supports the separation of different information (modularity)

How to identify Layers?
- they begin with `meta-` and are found in the *Source Directory*

---

### Yocto ***RECIPES***

> Recipe file = contains all the information about the unit (piece of software that is to be built) such as: dependencies, source file locations, checksums, description and so on.

Contain:
- Descriptive information about the package (author, homepage, license, and so on)

- The version of the recipe

- Existing dependencies (both build and runtime dependencies)

- Where the source code resides and how to fetch it

- Whether the source code requires any patches, where to find them, and how to apply them

- How to configure and compile the source code

- How to assemble the generated artifacts into one or more installable packages

- Where on the target machine to install the package or packages created
---

### Yocto ***BITBAKE***
- initially part of the OpenEmbedded project

> Bitbake = a task executor, a build tool
- allows shell and Python tasks to be run
- takes some metadata and executes tasks w.r.t them
- can take code from local/remote
- is a program written in Python, controls how software is built
Metadata

|Type of file|Explanation|
|-|-|
|.bb|recipe
|.bbappend|related recipe
|.conf|configuration
|.inc|undelying include
|.bbclass|class files|

---

## What is a petalinux though?

A wrapper over yocto -> used by Xilinx to ease the usage of yocto on their boards

- now petalinux doesn't have many packages installed (for space optimization)

## What does petalinux-build do?

- starts from the "smallest" to the "biggest" components (FSBL)

- **Output**: SDK (cross-compiler - could host app development), images

## Device Tree

- in kernel exista mai multe drivere care sunt/nu activate, dar e nevoie si de locatia perifericului pe care dorim sa il accesam. 

> Fisier dinamic care contine informatii legate de platforma pe care lucram (registers' addresses, width, no. of registers, compatible driver). Structured like a tree. Basically a hardware platform definition.

`.dtsi .dts files` - C syntax

Remark : **uart** seems to be disabled in the device system tree file, status = "disabled" so the kernel doesn't use that at boot time. In other files, its status seems to be okay => flag in the system file is overwritten.

`pcw.dtsi` - looks at all the peripherals 

`pl.dtsi` - linked to the .xsa

`system-user.dtsi` - fully configurable by us (activate components/disable stuff, modifications) - ***Our sandbox***
/home/digilent/Zybo-Z7-2022-OS/project-spec/meta-user/recipes-bsp/device-tree/files

# PWM project

- in user space on PUTTY
## Write directly into registers

- use busyBox utilitary
- use devmem command
- find addresses from device tree

- figure out that the the gpio is set to input / output

## Use driver
- navigate to driver position and echo stuff
- check 

### LEDS gpio driver
- make out gpio compatible to the new driver

- more info on the xilinx repo

# Homework:
1. Script :white_check_mark:
- bash script to control the gpio-s using switch and buttons
- implement some functions  (could write it in vi editor but won't remain : vi leds.sh)
- could also place it on the sd card
`ls media/sd0m...`
-  use echo, cat ... 

- put mkdir gpio_bash in `/project-spec/meta-user/recipes-apps`

2. To run  `petalinux build --sdk` :white_check_mark:

3. Read about Yocto (watch) :white_check_mark:

4. Prepare Ethernet cable to connect the Zybo to the Router (a router able to give the Zybo the IP address) sau la calculator daca avem configurat un server de DHCP (care da IP uri).

### When is the club over?
- 24 may
