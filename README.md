# RPi_SPI_DTS_kernel_overlay
Device Tree overlay for Raspberry Pi 2/3/4/Zero - adding more /dev/spidev devices
Tested on Raspian Buster, kernel 4.19.97

By default RPi allows us to use 2 spidev devices on GPIOs 8 and 7(/dev/spidev0.0 and /dev/spidev0.1), so only 2 modules can communicate with it by SPI Interface.
The overlay lets SPi driver to use other RPi GPIOs as SPI. The example .dts file targets GPIOs: 2 3 27 19 13 6 5 17 21

## Install
In directory, where spi-overlay.dts is saved:

```
$ dtc -@ -I dts -O dtb -o spi-overlay.dtbo spi-overlay.dts
$ sudo spi-overlay.dtbo /boot/overlays

```
Then, edit /boot/config.txt
1. Comment line 
```
#dtparam=spi0=on

```
2. Add at the end of the file:
```
dtoverlay=spi-overlay

```
Reboot and check
```
$ sudo reboot
$ ls /dev/spidev*
/dev/spidev0.0  /dev/spidev0.1  /dev/spidev0.3 /dev/spidev0.4  /dev/spidev0.5 /dev/spidev0.6  /dev/spidev0.7  /dev/spidev0.8 /dev/spidev0.9  /dev/spidev0.10

```
