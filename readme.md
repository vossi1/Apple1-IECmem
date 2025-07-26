# Apple1-IECmem Apple IEC/RAM/ROM/IO-card

**Copyright (c) 2025 Vossi - v 1.0**
**www.mos6509.com**

## License
This work is licensed under a Creative Commons Attribution-ShareAlike 4.0
International License. See [https://creativecommons.org/licenses/by-sa/4.0/](https://creativecommons.org/licenses/by-sa/4.0/)

**screenshots:**

![screen1](https://github.com/vossi1/Apple1-IECmem/blob/master/photos/screen1.jpg) ![screen2](https://github.com/vossi1/Apple1-IECmem/blob/master/photos/screen2.jpg) ![screen3](https://github.com/vossi1/Apple1-IECmem/blob/master/photos/screen3.jpg)

**description:**

    Apple1 expansion card with these features:

    - replaces or extends the onboard RAM to 4x 32KB bankswitched sram
    - up to 2x 32KB ROM (replaces optional the onboard PROMs)
    - * AT29c256 for 32KB or W27c512 for 2x 32KB switchable
    - VIA 65c22 with 8 bit Userport
    - Commodore-compatible IEC interface (JD) (1541, 1571, 1581, ...)
    - onboard SD2IEC
    - IEC interpreter in C400-CFFF
    - compatible with ACI (load from tape -> save to disk and vice versa)
    - compatible with Wendell Sander's Expansion board (unbufferd mode!)

**ROMs**

    iec.bin         only the IEC interpreter at C400-CFFF
    rom.bin         32K image with IEC @C400, Basic @E000, 16xWozmon @F000
    rom_nojd.bin    - same but without floppy speeder routines
    rom64.bin       64K 2x rom.bin but upper half with Krusader

**[Schematic](https://github.com/vossi1/Apple1-IECmem/blob/master/schematics_v10.png)**

**[Parts](https://github.com/vossi1/Apple1-IECmem/blob/master/parts_v10.txt)**

![front](https://github.com/vossi1/Apple1-IECmem/blob/master/photos/front.jpg)

![back](https://github.com/vossi1/Apple1-IECmem/blob/master/photos/back.jpg)

**commands:**

    C400R               start IEC-Interpreter ('#' symbol)

    L"FI*               loads file to address in first two file-bytes
    L"FILE",8           loads from device 8
    R"FILE",9,280       load+run file to 0280
    V"FILE",A,2000      verifys file with memory from 2000
    S"FILE",8,280,FFF   saves file to device 8 from 0280 to 0FFF
    U8                  changes the default unit
    I9                  changes the device ID of the SD2IEC temporary
    B0                  switches to RAM bank 0 (3 is default at startup)
    D                   prints the directory
    DTEST*              prints all files beginning with TEST
    @                   prints the device status (device selected with U#)
    @S:TEST             sends disk command to device selected with U#

    Commands can be interrupted with ESC
    After resetting, the default device and the selected RAM bank remain unchanged!

**DIP-switches:**

    1   enables 8KB RAM 0000-1FFF (onboard RAM pulled or A1 X+W solderpads open!)
    2   enables 8000-9FFF in Eprom
    3   enables A000-AFFF in Eprom
    4   enables B000-BFFF in Eprom
    5   enables C400-CFFF in Eprom (Here is my IEC-interpreter)
    6   enables E000-EFFF in Eprom (Here is the Basic)
        * you can disable this, connect W to E on A1 board and use RAM here
    7   enables F000-FFFF in Eprom (Proms A1+A2 pulled or Y solderpad on A1 open!)
    8   on for 29C256 VPP @+5V, on=A15 HI for W27c512 (parralel to toggle switch) 

**comments:**

    I accidentally used 0603 footprints for C1-C4, but 0805 can also be used.
    JD currently not running reliable with external drives.
    An IEC connector hits the power connector when the card is plugged directly into the Board.
    The toggleswitch is optional to switch between w27c512 lower/upper half.
    It's also possible to leave the SD2IEC parts away and use an external device only.
    The Userport connector is optional, but it doesn't prevent the use of a PLCC extractor.
