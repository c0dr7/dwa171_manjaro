# rtl8821CU

Drivers for rtl8811CU and rtl8821CU Wi-Fi chipsets forked from [uzh-rpg/rpg_dwa171_wifidongle](https://github.com/uzh-rpg/rpg_dwa171_wifidongle) so its ready for manjaro, forked from [whitebatman2/rtl8821CU](https://github.com/whitebatman2/rtl8821CU). 


This repository is based on soruce code found on a CD shipped with a rtl8811CU based card. It's updated to build on newer kernel versions. A simple line was added to allow this driver to work with the latest hardware revision of the DWA-171 C1 wifi dongle!

## Mind the architecture: i386 or ARM?
You might need to set correct the platform in the Makefile.

For Intel, change it to:
```
CONFIG_PLATFORM_I386_PC = y
CONFIG_PLATFORM_ARM_RPI = n
CONFIG_PLATFORM_ARM_RPI3 = n
```
For ARMv7:
```
CONFIG_PLATFORM_I386_PC = n
CONFIG_PLATFORM_ARM_RPI = y
CONFIG_PLATFORM_ARM_RPI3 = n
```
For ARMv8:
```
CONFIGx_PLATFORM_I386_PC = n
CONFIG_PLATFORM_ARM_RPI = n
CONFIG_PLATFORM_ARM_RPI3 = y
```

## Build and install without DKMS
Use following commands in source directory:
run
```
uname -r
```
you will see your kernel version
then you need to get headers, if its 4.19
```
sudo pacman -S linux419-headers
```
then you are ready to:
```
make
sudo make install
sudo modprobe 8821cu
```

## Final step: add this script!!!
The USB Wifi Dongle has a small storage partition with the Windows drivers inside that gets mounted before the wifi adapter itself. Follow these steps to ensure the Wi-Fi adapter is mounted with the stick is inserted!

```
chmod +x automountDWA171-manjaro.sh
sudo ./automountDWA171-manjaro.sh
```
You're done, you can plug the dongle!

