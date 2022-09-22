---
tags: [Notebooks/Digilent]
title: "Course Notes 17.05.2022 \U0001F41D"
created: '2022-05-17T13:35:52.515Z'
modified: '2022-05-24T12:04:07.212Z'
---

# Course Notes 17.05.2022 :bee:

## Homework feedback:
- pretty nice, can integrate the heartbeat led-s
- remember to power off the VM from "inside"

## De legat la pc using ethernet Cable =
- internet connection sharing dam la o alta retea -> internet sharing pentru reteaua de pe WIFI pe reteaua cablata.
- control panel -> network status and... -> wifi/properties/sharing check allow other users... select ethernet -> ethernet/details/ copy the IP :white_check_mark:

# Today
# First Part Vitis C project
- use the sdk build
`images/linux/sdk/sysroots` => archive folder

- vitis zynq workspace => create new platform (linux instead of bare-metal): **linux_pf**
  - need to add .bif file (boot information)
  - boot components (referenced by the bif file): system.bit (design wrapper-ul actually), zynq_fsbl.elf, u-boot.elf, system.dtb

- create new vitis project
  - inside the sysroots we have some sort of rootFS containing no symbolic links
  `symbolic links` (more in the video), but the important thing is that we have the libraries

- debug as... set configurations and connect board to ethernet
IP: 192.168.137.156/24
  - set target connection (add board IP)
  - daca vrem sa avem doar o consola pentru vitis project (fara kernel messages)=> connect to PUTTY prin SSH (cu IP ul placii);
  - putem rula din /mnt/sd.../ (output file)

## Remarks
- symbolic links in rootfs not working (broken links)

# Second Part Customize the rootFS

- hello-world becomes treated as a sysCall
- customize the rootFS plnx doc chapter 8

## Add a custom application
- initial not enabled
- we get a new directory containing the app (to be installed at boot time)
- Add our .c source inside it
- manually config petalinux to enable the app
- build & package


## Homework

- make sure all works well :white_check_mark:

1. create a C program to access LEDs, buttons, switches (access the gpio(s), adapt the bash program ish)

Hints: 

- not easy - lucram cu manipulare de fisiere, ensure that resources are not accesses by another process. Ce putem sa mai facem.

`project-spec/meta-user/recipes-bsp/device-tree/files/system-user.dtsi` - Putem muta heartbeat driver ul care sa foloseasca pin ul de la LD4 (git la Robert)

- pe git-ul lui elod - rezolvare cu system-user.dtsi

`project-spec/meta-user/recipes-apps/gpio-demo/files/gpio-demo.c`
- in recipes-apps avem gpio-demo / files / avem un exemplu de accesare a gpio resources

- sa aiba fiecare led un subnod ca la heartbit (1:41:00) - can use documentatie de referinta dtbidings on github

- use define statements (more explainations)

---

2. After we have the Vitis app, generate a new project and copy in the generated cfile the code. Enable from rootfs, build (sau punem direct in hello-world)

# Next time
- control pwm ip thourough

# Documentation UIO main points

## Who can host UIO? Userspace Input-Output System
- The device has memory that can be mapped. The device can be controlled completely by writing to this memory.
- The device usually generates interrupts.
- The device does not fit into one of the standard kernel subsystems.

## Accessing UIO
- through device file (/dev/uioX)

### Read an interrupt
- use read() / select() / from uioX
- to prevent unknown interrupt sources make the kernel disable IRQ

### Re-enable interrupts
- write(), irqcontrol() (to be implemented by driver)
- we can also have a custom interrupt handler

- uio_event_notify() - simulates interrupts

### Memory mapping
- UIO device can make accesssible regions for memory mapping

Can also have info about ports

## Kernel module (how to write):
- use struct uio_info + struct_uio_mem (memory regions to be mapped)

## From user space
- can write programs to use the kernel uio module
- get information(name/version)
- mmap device memory
- wait for interrupts
