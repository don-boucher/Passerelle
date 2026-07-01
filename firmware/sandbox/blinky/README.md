## Install Dependencies
```
sudo pacman -S git cmake ninja gperf ccache dfu-util dtc wget \
    python-pip python-setuptools python-wheel tk xz file make which
```

## Application Creation
```
mkdir blinky
cd blinky
git clone https://github.com/zephyrproject-rtos/example-application application
west init -l application
west update
cd application
rm -rf .git .github .gitignore
## replace contents of blinky/application/app/src/main.c with blinky
## add `CONFIG_GPIO=y` to blinky/application/app/prj.conf
```

## Fetch Project Dependencies
```
west update
```

## Build
```
west build -p always -b nrf7002dk/nrf5340/cpuapp application/app
```

## Flash
```
west flash
```

## Debug
```
west debug
```
```
[don@Mothman blinky](main)$ west debug
-- west debug: rebuilding
ninja: no work to do.
-- west debug: using runner jlink
reset after flashing requested
JLink version: 9.54
J-Link GDB server running on port 2331; no thread info available
SEGGER J-Link GDB Server V9.54 Command Line Version

GNU gdb (Zephyr SDK 1.0.1) 16.2
Copyright (C) 2024 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "--host=x86_64-build_pc-linux-gnu --target=arm-zephyr-eabi".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://github.com/zephyrproject-rtos/sdk-ng/issues>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/zephyr.elf...
No core file specified.
JLinkARM.dll V9.54 (DLL compiled Jun 25 2026 17:34:42)

-----GDB Server start settings-----
GDBInit file:                  none
GDB Server Listening port:     2331
SWO raw output listening port: 2332
Terminal I/O port:             2333
Accept remote connection:      yes
Generate logfile:              off
Verify download:               off
Init regs on start:            off
Silent mode:                   on
Single run mode:               on
Target connection timeout:     0 ms
------J-Link related settings------
J-Link Host interface:         USB
J-Link script:                 none
J-Link settings file:          none
------Target related settings------
Target device:                 nrf5340_xxaa_app
Target device parameters:      none
Target interface:              SWD
Target interface speed:        4000kHz
Target endian:                 little

Remote debugging using :2331
main () at /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/include/generated/zephyr/syscalls/device.h:55
55              compiler_barrier();
Resetting target
Loading section rom_start, size 0x154 lma 0x0
Loading section text, size 0x4a40 lma 0x154
Loading section initlevel, size 0x48 lma 0x4b94
Loading section device_area, size 0x70 lma 0x4bdc
Loading section sw_isr_table, size 0x228 lma 0x4c4c
Loading section device_api_area, size 0x4c lma 0x4e74
Loading section rodata, size 0x620 lma 0x4ec0
Loading section datas, size 0xc0 lma 0x54e0
Loading section device_states, size 0x8 lma 0x55a0
--Type <RET> for more, q to quit, c to continue without paging--c
Loading section .last_section, size 0x4 lma 0x55a8
Start address 0x00000934, load size 21932
Transfer rate: 4 KB/sec, 2193 bytes/write.
Resetting target
(gdb) break main
Breakpoint 1 at 0x154: file /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/include/generated/zephyr/syscalls/device.h, line 55.
(gdb) c
Continuing.

Breakpoint 1, main () at /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/include/generated/zephyr/syscalls/device.h:55
55              compiler_barrier();
```