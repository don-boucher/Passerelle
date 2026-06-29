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
JLinkGDBServer -if swd -device nRF5340_xxAA_APP
```
From another shell:
```
arm-none-eabi-gdb build/zephyr/zephyr.elf
```
```
(gdb) target extended-remote:2331
Remote debugging using :2331
0x00003cd6 in arch_cpu_idle ()
    at /home/don/repos/passerelle/firmware/sandbox/blinky/zephyr/arch/arm/core/cortex_m/cpu_idle.c:99
99              SLEEP_IF_ALLOWED(__WFI);
(gdb) monitor halt
(gdb) monitor reset
Resetting target
(gdb) break main
Breakpoint 1 at 0x154: file /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/include/generated/zephyr/syscalls/device.h, line 55.
(gdb) c
Continuing.

Breakpoint 1, main ()
    at /home/don/repos/passerelle/firmware/sandbox/blinky/build/zephyr/include/generated/zephyr/syscalls/device.h:55
55              compiler_barrier();
```