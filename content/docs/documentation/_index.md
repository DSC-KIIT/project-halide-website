---
weight: 2
bookFlatSection: true
---

# HalideOS - Technical Documentation

[github.com/DSC-KIIT/project-halide](https://github.com/DSC-KIIT/project-halide)

**HalideOS** is an experimental operating system, written from scratch by the OS team at DSC KIIT. The main motive of this
project was to build a basic yet functional operating system from scratch and demonstrate some of the basics of OS theory. 

If you're new to OS development then please refer the **Getting Started** section of this website.

This part of the website contains technical documentation for some of the important components of HalideOS, the content here 
will act as an aid to help you understand the source code. HalideOS is written in C++17 with some x86 assembly code for the boot procedure and interrupts.

The diagram below represents all the components that come together to make HalideOS work. The best way to understand how Halide does what it does is to read through the source code and keep these docs handy.

<br>

![Main Diagram](/project-halide/diagram.png)

<br>

## Boot Up

The boot procedure is implemented in the `src/loader.s` file. We used the multiboot specification to boot using the GRUB bootloader. 
After the bootloader transfers control to our OS, we setup the stack so that our C++ code has memory to run on. 

After this, the `k_main` function is called which is the entry point for the kernel.


## Kernel

Implemented in `src/kernel.cpp`

As Halide is a pretty simple OS, all the components comes together in the kernel and are executed from the kernel itself, there is no seperation of user mode and kernel mode. All the further components are imported, initialized and executed from the kernel.

## Global Descriptor Table

Implemented in `include/globaldescriptortable.h `  and `src/globaldescriptortable.cpp`

These files contain the standard boilerplate code to setup memory segmentation using the Global Descriptor Table. This is explained in more detail in [here](https://littleosbook.github.io/#segmentation)


## Interrupt Descriptor Table

Implemented in `src/interrupts.h` and `src/interrupts.cpp`. You can read up more about how interrupts work in x86 processors [here](https://littleosbook.github.io/#interrupts-and-input)


## FrameBuffer and Window

This is an abstraction for the framebuffer device that the BIOS provides us so that we can output text on the screen. You can read more about it [here](./Frame%20Buffer.md)

The Window class is just a collection of x and y coordinates with some functions to restrict the cursor on the framebuffer so that the we can divide up the screen and implement a notion of multiple windows. You can read more about it [here](./Windows.md)


## Console

Implemented in `include/console.h` and `src/console.cpp`

This part of the code enables the user to type in commands in the console and get the results. A detailed explaination of the 
console is given [here](./Console.md)


## Halide Standard Library

Implemented in `include/halidestdlib.h` and `src/halidestdlib.cpp`

A set of some standard data structures and functions used to implement features and console commands. You can read about it
[here](./Standard%20Library.md)
