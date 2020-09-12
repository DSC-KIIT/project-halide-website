# Introduction to Operating Systems Development

<center><h3>Please proceed with a <b>really good</b> grasp of C/C++</h3></center>

If you landed here then, congratulations! You are about to take on one of the most challenging projects in Software Engineering, that is, Operating System Developement. There are no proper roadmaps, no copy-paste code and lots of theory. You'll be guided solely by passion and you will truly peak once you dive into the depths of OS Dev.

You need to be able to understand how hardware works, read and write assembly code to boot up your kernel and fairly good C/C++ code to add other features. It will require time, patience and careful code designs filled with abstractions.

If the prerequisites sound overwhelming, maybe this is not the right time for you to get into OS Dev. It's not a week-long project that you can just be done with. It may takes months of work to take care of every possible test case for one typo, one loophole, will be enough to break your system. in short, this is an ongoing process.

Finally, this is not the guide to make the next Linux or Windows. This is a beginners guide based on our mistakes and learnings as we proceeded to make the experimental **Halide OS**.

## Contents -

1. Motivation
2. Rules and Goals
3. Basic Definitions
4. Essential Tools
5. Choose your Development Environment

### Motivation

> When you write a program and it runs too slow, but you see nothing wrong with your code, where else will you look for a solution. How will you be able to debug the problem if you don’t know how the operating system works? Are you accessing too many files? Running out of memory and swap is in high usage? But you don’t even know what swap is! Or is I/O blocking?

While we've established that a serious software engineer should know how operating systems works, the extent of this knowledge can be questioned, but knowing how your programs interact with the system will help you code more efficient and sophisticated programs. It's a powerful feeling plus a great learning experience to add features and optimizations that you need in an OS. Moreover working with low-level languages is always a fun and exciting task.

### Rules and Goals

It is not okay to write poor code thinking that the computer will take care of it because that's the job of the operating system itself. You need efficient error handling, programs which don't hog all the memory and are as concrete and simple as possible. Needless to say, these qualities come with experience.

Also, have a plan as in what exactly do you want your system to do? You cannot program your system to work like a commercial OS because it is way too broad. So be specific but be ambitious. You should have a clear idea of your codebase and your end goal of whether you want to build a terminal or GUI or something else altogether.

### Basic Definitions

#### [Operating System](https://en.wikipedia.org/wiki/Operating_system)

In the Kingdom of Hardware, the national language is machine code comprising of 0's/1's, on's/off's etc. But since it was useless on its own, it was merged with the Kingdom of Software where everyone spoke various low to high-level languages. This led to mass confusion as the Hardware residents couldn't understand Software residents and vice-versa. To solve this problem, a translator called Operating System was called.

An Operating System is a framework that tells your computer how to use its hardware. Specifically, it hides hardware complexity, manages memory and other system resources, schedules and multiplexes processes and threads, provides a basic user interface and application programmer interface, also focussing on isolation and protection. Not every Operating System in the market provides all these functionalities. Therefore you have to be clear with your goals.

Some popular examples include [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows) which has a huge user base, [Linux](https://en.wikipedia.org/wiki/Linux) which is lightweight because of small, specific components ([distributions](https://en.wikipedia.org/wiki/List_of_Linux_distributions)) making it highly customizable but less user-friendly and the [BSD triplets](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution) for server related tasks.

#### [Kernel](<https://en.wikipedia.org/wiki/Kernel_(operating_system)>)

> The kernel is like a traffic cop. It stands between your computer's hardware and the applications that you want to run. It allocates memory, keeps track of file systems on your disk drives, and it divides up time so that each program gets its turn to use your computer's resources.

Operating systems are mostly about drivers. That's more than 90% of a kernel. So a kernel is the core of an OS that is invisible and the only time you'll see it is when it [panics](https://en.wikipedia.org/wiki/Kernel_panic), calls in backup and arrests everyone in case there's a crime going on.

#### [Shell](<https://en.wikipedia.org/wiki/Shell_(computing)>)

A shell is a program which acts as an interface between humans and the kernel. Since we cannot talk to this program directly, we can use commands (command line) or a mouse (file explorer) to perform basic tasks like starting a program, managing files, etc. But where do we write these commands? That's where the [Terminal](https://en.wikipedia.org/wiki/Computer_terminal#:~:text=A%20computer%20terminal%20is%20an,a%20computer%20screen%20by%20decades.) comes in which tells the shell what to do.

#### [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface)

A Graphical User Interface is the visible part of an Operating System that helps you modify the features of your Operating System. It does that via graphics as opposed to textual interfaces like the [Terminal](https://en.wikipedia.org/wiki/Computer_terminal#:~:text=A%20computer%20terminal%20is%20an,a%20computer%20screen%20by%20decades.). A GUI simply redraws parts of the screen depending on the user input solving the blank screen problem found in early Operating Systems. This provides a better user interface.

#### Emulation and Virtualization

Virtualization is like moving into a house that already has basic utilities like plumbing electricity, etc whereas Emulation is where you're basically building a house from scratch.

The purpose of an [Emulator](https://en.wikipedia.org/wiki/Emulator) is to accurately reproduce the behavior of some hardware for seeking independence from the hardware of the host machine. We want to do this for testing purposes since we want our Operating System to be hardware-independent.

While emulated environments require a software bridge to interact with the hardware, [Virtualizers](https://en.wikipedia.org/wiki/Virtualization) access hardware directly. However, despite being the faster option, virtualization is limited to running software that was already capable of running on the underlying hardware.

### Essential tools

- [GNU Compiler Collection](https://wiki.osdev.org/GCC) - To provide compilers for programming languages like C, C++, etc.
- [Assembler](https://en.wikipedia.org/wiki/Assembly_language#Assembler) - Like [NASM](https://www.nasm.us/) or [GAS](https://en.wikipedia.org/wiki/GNU_Assembler) depending upon your CPU architecture.
- [Make](https://wiki.osdev.org/Makefile) - For automating the build process.
- [Binutils](https://www.gnu.org/software/binutils/) - For object file manipulation.
- [Emulator](https://en.wikipedia.org/wiki/Emulator) - [QEMU](https://www.qemu.org/) or [Bochs](https://en.wikipedia.org/wiki/Bochs) for testing.
- [Version Control](https://en.wikipedia.org/wiki/Version_control) - Like [Git](https://en.wikipedia.org/wiki/Git) to protect your code.
- [Text Editor](https://wiki.osdev.org/List_of_editors) - Like [Vim](https://www.vim.org/) or [VS Code](https://code.visualstudio.com/) for writing all your code.

### Choose your Development Environment

#### GNU/Linux

All the development tools are already present and if not, they can be easily installed with a package manager depending on your distribution.

#### Windows

[Cygwin](https://wiki.osdev.org/Cygwin) is strongly suggested to get you all the required tools and a Linux-like experience. Or you can use the new [Windows Subsystem for Linux](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) to not compromise on Windows features.

Whatever you choose, it is essential for you to build a [cross-compiler](https://wiki.osdev.org/GCC_Cross-Compiler) otherwise you'll run into a lot of problems.

<hr />

Now, that you know what's required and what's at stake, we wish you good luck in case you choose to embark on this demanding yet exciting journey of OS Development.
