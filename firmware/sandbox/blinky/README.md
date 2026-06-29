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

## Build
```
west build -b nrf7002dk/nrf5340/cpuapp application/app
```

## Flash
```
west flash
```