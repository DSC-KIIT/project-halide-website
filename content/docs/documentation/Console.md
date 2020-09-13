# Console Commands in HalideOS

The console in Halide is pretty simple. Just a while loop that evaluates the the commands entered by the user
using a big nested if-else, and then defers execution of the command to the proper functions.

- Files: `include/console.h` and `src/console.cpp`

The console supports the following commands

- `about`
- `help`
- `greet`
- `calculator` - A basic command line calculator
- `clear`
- `switch console` - Switches to the next console

Refer the `src/console.cpp` file to look at the implementation of these commands. Most of them are pretty simple as they just
print text on the framebuffer.

The `calculator` is the only command that does some work, it evaluates the passed expression and returns the results.
We implemented a standard infix to postfix converter and evaluated that postfix expression. The calculator is the reason we implemented a stack abstraction in the standard library.
