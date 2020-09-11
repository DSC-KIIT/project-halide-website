# The Frame Buffer

HalideOS uses the APIs provided by the BIOS to display text on the screen. We did not implement 
drivers for the graphics hardware to keep the code simple. BIOS implements a combination of 
memory-mapped I/O and I/O ports system to manipulate the screen and display the text.

## Memory Mapped I/O and I/O Ports

There are usually two different ways to interact with the hardware, memory-mapped I/O and I/O ports.

If the hardware uses memory-mapped I/O then you can write to a specific memory address and the hardware will be updated 
with the new data. One example of this is the **framebuffer**. For example, if you write the value `0x410F` to address `0xB8000`, 
you will see the letter A in white color on a black background, will explain this in later sections.

If the hardware uses I/O ports then the assembly code instructions `out` and `in` must be used to communicate with the hardware. 
The instruction out takes two parameters: the address of the I/O port and the data to send. The instruction in takes a single parameter, 
the address of the I/O port, and returns data from the hardware.

## What is the FrameBuffer ?

The framebuffer is a hardware device that is capable of displaying a buffer of memory on the screen. It has 80 columns 
and 25 rows, and the row and column indices start at 0 (so rows are labelled 0 - 24). You can think of it as a 2D matrix of 80x25.

### Displaying Text on the Screen

The starting address of the memory-mapped I/O for the framebuffer is `0xB8000`. The memory is divided into 16 bit cells, where the 16 bits determine both the character, the foreground color and the background color. 

The highest eight bits is the ASCII value of the character, bit 7 - 4 the background and bit 3 - 0 the foreground, as can be seen in the following figure:

```
Bit:     | 15 14 13 12 11 10 9 8 | 7 6 5 4 | 3 2 1 0 |
Content: | ASCII                 | FG      | BG      |
```

There are a set of 15 colour codes for foreground and background, these are hardcoded in the driver

### Moving the Cursor

Moving the cursor of the framebuffer is done via two different I/O ports. 

The cursor’s position is determined with a 16 bits integer: 
* 0 means row zero, column zero 
* 1 means row zero, column one
* 80 means row one, column zero and so on. 

Since the position is 16 bits large, and the out assembly code instruction argument is 8 bits, 
the position must be sent in two turns, first 8 bits then the next 8 bits. 

The framebuffer has two I/O ports, one for accepting the data, and one for describing the data being received. Port `0x3D4` is the port that describes the data and port `0x3D5` is for the data itself.

On `0x3D4`:
* Writing the integer `14` tells the framebuffer to expect the highest 8 bits of the position
* Writing the integer `15` tells the framebuffer to expect the lowest 8 bits of the position

<br>

---

## The FrameBuffer driver in HalideOS

The driver is encapsulated in the `FrameBuffer` namespace. It has 2 components, `FrameBuffer::Colours` namespace has all the hex codes for the supported colours and the `FrameBuffer::Writer` class has all the functions to manage the cursor and the text on the framebuffer.

* Files : `include/frame_buffer.h` and `src/frame_buffer.cpp`
* Namespaces: `FrameBuffer`, `FrameBuffer::Colours`
* Classes: `FrameBuffer::Writer`

### `FrameBuffer::Colours`

{{< expand "All available colours - Click to expand" >}}
```C++
namespace Colours {
	static const unsigned char BLACK = (unsigned char)0x0;
	static const unsigned char BLUE = (unsigned char)0x1;
	static const unsigned char GREEN = (unsigned char)0x2;
	static const unsigned char CYAN = (unsigned char)0x3;
	static const unsigned char RED = (unsigned char)0x4;
	static const unsigned char MAGENTA = (unsigned char)0x5;
	static const unsigned char BROWN = (unsigned char)0x6;
	static const unsigned char LIGHT_GREY = (unsigned char)0x7;
	static const unsigned char DARK_GREY = (unsigned char)0x8;
	static const unsigned char LIGHT_BLUE = (unsigned char)0x9;
	static const unsigned char LIGHT_GREEN = (unsigned char)0xa;
	static const unsigned char LIGHT_CYAN = (unsigned char)0xb;
	static const unsigned char LIGHT_RED = (unsigned char)0xc;
	static const unsigned char LIGHT_MAGENTA = (unsigned char)0xd;
	static const unsigned char LIGHT_BROWN = (unsigned char)0xe;
	static const unsigned char WHITE = (unsigned char)0xf;
} // namespace Colours
```
{{< /expand >}}


### `FrameBuffer::Writer`

**Functions (all public)**

* `Writer(const unsigned char &foreground, const unsigned char &background, Window*)`
* `void clearLine(unsigned char from, unsigned char to)`
* `void clearScreen()`
* `void initScreen(const unsigned char &foreground, const unsigned char &background)`
* `void setColorTheme(const unsigned char &foreground, const unsigned char &background)`
* `void writeString(char *str, unsigned char = FrameBuffer::Colours::WHITE)`
* `void writeHex(unsigned char key)`
* `void fillRemeaning(char *, bool)`
* `void writeAtIndex(int)`
* `void switchWindow(Writer &)`
* `void clearCursor()`
* `void shiftCursor(int, char *)`
* `void updateCursor()`
* `void Rerender(Window*)`


Refer the source code for more details on the implementation.

<br>

### References

* https://littleosbook.github.io/#output