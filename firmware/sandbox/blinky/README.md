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
```