# Running and Compiling HalideOS on your System

## Running HalideOS in Oracle Virtual Box

1. Head over to the [Releases](https://github.com/DSC-KIIT/project-halide/releases) section of the GitHub repository and download the `halide.iso` file.

![s1](/project-halide/s1.png)

2. Open up [Oracle VM VirtualBox](https://www.virtualbox.org/). Click on **New**.

![s2](/project-halide/s2.png)

3. Put HalideOS as the name. Set **Type** to **Other** and **Version** to **Other/Unknown**.

![s3](/project-halide/s3.png)

4. Set the memory size. 64 MB will be enough.

![s4](/project-halide/s4.png)

5. Click on Next and select **Do not add a virtual disk** and click on **Create**.

![s5](/project-halide/s5.png)

6. You will see an instance created. Now we need to load the `halide.iso` file we just downloaded. For that, navigate to **Settings**.

![s6](/project-halide/s6.png)

7. Under **Settings**, go to **Storage** and click on the **Empty** option in the left pane.

![s7](/project-halide/s7.png)

8. Click the CD like **icon** next to **IDE Secondary Master**.

![s8](/project-halide/s8.png)

9. Choose the `halide.iso` file.

![s9](/project-halide/s9.png)

10. Then click **OK**.

![s10](/project-halide/s10.png)

11. You are all set, just click on **Start** to fire up HalideOS.

![s11](/project-halide/s11.png)

12. Put your name as the username. Password is `dsc-kiit`

![s12](/project-halide/s12.png)

13. Press Enter

![s13](/project-halide/s13.png)

14. You will be logged in and a console will be setup for you

![s14](/project-halide/s14.png)

Congratulations, you just booted into HalideOS!

### Commands

These are the commands that are available in the HalideOS console:

- `about` - Know more about HalideOS
- `help` - Get a list of all available commands
- `calculator` - A basic calculator that can evaluate expressions like `10-3*2` (don't put spaces or brackets)
- `greet` - Get a greeting
- `clear` - Clears the console
- `switch window` - Switches to the next window

Try them out for yourself.

If you're curious then the source code for halide is available at https://github.com/DSC-KIIT/project-halide

---

## Compiling HalideOS from Source

This section will help you with setting up your development environment so that you can compile the code for HalideOS yourself and run it in an emulator. This is a good place to start if you are intersted in contributing code to the project.

### Dependencies

It is recommended that you used a Linux based operating system for building HalideOS. The C/C++ development
tools and the entire ecosystem is much easier to use on a Linux based system.

- `g++` - A C++ compiler
- `nasm` or `as` - An x86 assembler
- `ld` - The GNU Linker
- `make` - GNU Make, a build tool for Linux
- `qemu` - An x86 Emulator
- `git` - For version control
- A text editor of your choice. We use Visual Studio Code

You can Google up how to install these tools for your host operating system. On Linux based systems you will
mostly install them using your package manager.

Once you have all these set up on your machine, run the following commands

```shell
git clone https://github.com/DSC-KIIT/project-halide
cd project-halide/src
make run
```

This will compile and build `kernel.iso` in the `src/` directory and start it in `qemu`.

You can run `make help` to get a list of all the commands available for various stages of compilation.

Please refer to the [Documentation](../../documentation/_index.md) section of the website for more details on the design and the code.
