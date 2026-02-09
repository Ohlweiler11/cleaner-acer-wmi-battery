# cleaner-acer-wmi-battery

## Description

This repository contains an experimental Linux kernel driver for the
battery health control WMI interface of Acer laptops. 
It can be used to control two battery-related features of Acer laptops: health mode and
calibration mode. It can also be used to read the battery temperature.

A list of models on which the driver works can be found [here](MODELS.md).
Any feedback on how it works on Acer laptops not found on this list is appreciated.

## Building

On a Debian/Ubuntu system, you can build by:
```
sudo apt install build-essential linux-headers-$(uname -r) git
git clone https://github.com/Ohlweiler11/cleaner-acer-wmi-battery
cd acer-wmi-battery
make
echo acer-wmi-battery | sudo tee /etc/modules-load.d/acer-wmi-battery.conf
sudo mkdir -p /lib/modules/$(uname -r)/kernel/extra/
sudo cp acer-wmi-battery.ko /lib/modules/$(uname -r)/kernel/extra/
sudo depmod
sudo modprobe acer-wmi-battery
sudo cp battery /usr/local/bin
sudo chmod +x /usr/local/bin/battery
```
For other systems, use the equivalent command to install the kernel headers for your kernel installed and type.

## Using

### Health mode

Sets the charge limit to 80% to preserve battery's capacity.
To enable it:
```
sudo battery enable health-mode
```
To disable it:
```
sudo battery disable health-mode
```
To check its status:
```
sudo battery status health-mode
```

### Calibration mode

Puts your battery through a controlled charge-discharge cycle to provide more
accurate battery capacity estimates. Before attempting the battery calibration, connect
your laptop to a power supply.
To start it:
```
sudo battery start calibration
```
After it is finished, you will have to stop it manually by:
```
sudo battery stop calibration
```
To check its status:
```
sudo battery status calibration
```

### Battery temperature

The temperature of the battery can be checked by:
```
battery temperature
```

## Original project

This repository is largely based on [this](https://github.com/frederik-h/acer-wmi-battery) project, but redesigned to have the module be inserted on boot and cleaner commands. Check that repository for more information.