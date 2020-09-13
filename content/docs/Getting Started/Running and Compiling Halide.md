# Running and Compiling HalideOS on your System

## Running HalideOS in Oracle Virtual Box

The first step would be to head over to the [Releases](https://github.com/DSC-KIIT/project-halide/releases) section of the github repository and download the `halide.iso` file

![s1](/project-halide/s1.png)

The open up the Oracle VM Virtual Box program. Click on **New**

![s2](/project-halide/s2.png)

Put in the name as HalideOS. Set **Type** to **Other** and **Version** to **Other/Unknown**

![s3](/project-halide/s3.png)

Set the memory size. 64 MB shall be enough.

![s4](/project-halide/s4.png)

Click on Next and select **Do not add a virtual disk** and click on **Create**

![s5](/project-halide/s5.png)

You shall see an instance created. Now we need to load the `halide.iso` file we just downloaded. For that, navigate to **Settings**

![s6](/project-halide/s6.png)

Navigate to **Storage** and click on the **Empty** option in the left pane

![s7](/project-halide/s7.png)

Click the CD like icon next to "IDE Secondary Master"

![s8](/project-halide/s8.png)

Choose the `halide.iso` file

![s9](/project-halide/s9.png)

Click on OK

![s10](/project-halide/s10.png)

You are all set, just click on **Start** to fire up HalideOS.

![s11](/project-halide/s11.png)

Put your name as the username. Password is `dsc-kiit`

![s12](/project-halide/s12.png)

Press Enter

![s13](/project-halide/s13.png)

You will be logged in and a console will be setup for you

![s14](/project-halide/s14.png)

If all of these steps worked out the congratulations, you just booted into HalideOS. 

### Commands

These are the commands that are available in the HalideOS console:

* `about` - Know more about HalideOS
* `help` - Get a list of all available commands
* `calculator` - A basic calculator that can evaluate expressions like `10-3*2`, don't put spaces and brackets.
* `greet` - Get a greeting
* `clear` - Clears the console
* `switch window` - Switches to the next window

Try them out for yourself.

If you're curious then the source code for halide is available at https://github.com/DSC-KIIT/project-halide

---


## Compiling HalideOS from Source

### Dependencies

It is recommended that you used a Linux based operating system for building HalideOS. The C/C++ development
tools and the entire ecosystem is much easier to use on a Linux based system.

- `g++` - A C++ compiler
- `nasm` or `as` - An x86 assembler
- `ld` - The GNU Linker
- `make` - GNU Make, a build tool for Linux
- `qemu` - An x86 Emulator
- `git` - For version control
- A text editor of your choice, we use Visual Studio Code

You can Google up how to install these tools for your host operating system. On Linux based systems you will
mostly install them using your package manager.

Once you have all these set up on your machine, run the following commands

```shell
git clone https://github.com/DSC-KIIT/project-halide
cd project-halide/src
make run
```

This will compile and build `kernel.iso` in the `src/` directory and start it in `qemu`. 

You can try `make help` to get a list of all the commands available for various stages of compilation.

