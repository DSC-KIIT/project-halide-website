# The Keyboard Driver

The keyboard driver does the task of reading the input coming from the keyboard and writing it to the screen using the `FrameBuffer` driver. The keyboard driver uses I/O ports mapped to memory addresses `0x64` and `0x60` to read the data coming from the keyboard. 

Every time a key on the keyboard is pressed,  `0x64` is set and an 8 bit integer is available in `0x60` which is passed to a massive switch case that appropriately writes the text on the screen. The entered text is also stored in a character buffer, the pointer to this buffer is returned when the enter key is pressed.

The driver is wrapped in the `KEYBOARD_DRIVER` namespace with just one function,

* `char *readInput(FrameBuffer::Writer &p, int mode = 1)` 
  
  Returns a `char*` to the entered text while writing those characters to the `FrameBuffer::Writer` passed. 
  
  `mode=1` is normal mode and `mode=0` is password mode, just prints `*`.

Refer the source code for more details on the implementation.

