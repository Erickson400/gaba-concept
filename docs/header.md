# Header
The ROM header is decided by Gaba. The user does not need to touch it to create a Gaba ROM. It contains the following information.

### Entry Point
Has a jump instruction to your main procedure.
```
package main

main := proc() {

}
```
### Nintendo logo
The Nintendo bitmap image required for the boot procedure.

### Title
"GABAGAME"

### Manufacturer code
0

### CGB flag
0xC0 <br>
*CGB mode only*

### New licensee code
"00"

### SGB flag
0

### Cartridge type
0x1B <br>
*MBC5+RAM+BATTERY*

### ROM size
0x08 <br>
*Capacity: 8 MiB (8,388,608 bytes) <br>
Switchable Banks: 512, each with 16KiB (16,384 bytes) <br>*

### RAM size
0x04 <br>
*Capacity: 128 KiB (131,072 bytes) <br>
Switchable Banks: 16, each with 8 KiB (8,192 bytes) <br>*

### Destination code
0x01 <br>
*Overseas only*

### Old licensee code
0

### Mask ROM version number
0

### Header checksum
Automatically calculated.

### Global checksum
0

