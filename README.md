# AIC1106-IPcore

This is Altera Avalon IP core for TI TLV320AIC1106 PCM Codec With Microphone Amps & Speaker Driver.

#### Hardware:

The AIC1106 IP core receive/transmit audio data from/to CPU with standard Avalon staream sink/source.
Also the IP core have mode/status register implemented as Avalon memory mapped register.

Format of the mode/status register:</br>

Read:

| 31..6 | 5 | 4 | 3 | 2 | 1..0 |
| -- | -- | -- | -- | -- | -- |
| 0 | underflow_r | mute | reset_n | 0 | volume |

Write:

| 31..6 | 5 | 4 | 3 | 2 | 1..0 |
| -- | -- | -- | -- | -- | -- |
| 0 | reset | loopback | enable | mute | volume |


Normally, the stream sink/source interface should be connected to separate FIFO buffers implemented as on-chip FIFO memory.
The FIFO buffer, in turn, is connected to the system bus of the processor.

#### Software:

When FIFO buffers near to full/empty it fire interrupt and software driver is responsible for read/write FIFO buffers to keep audio staream continuouse.
During driver initialization, it registered as new device `/mnt/audio/` and being accessible as regular file.
Driver also capable to read/write standard .wav file.

For details, please explore files `audio_drv.c` and `audio_drv.h`

