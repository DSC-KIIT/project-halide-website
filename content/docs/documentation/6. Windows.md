# Windows in HalideOS

We have added support to divide the screen into multiple consoles. It is very similar to diving a linux terminal into multiple parts. This was done using a `Window` class that is passed to the `FrameBuffer::Writer` so that it can restrict the movement of the cursor in the limits defined in the `Windows` class.

* Files: `include/windows.h`

Its a pretty small class, everything is done in the header file, you can refer the source code to understand what it does.