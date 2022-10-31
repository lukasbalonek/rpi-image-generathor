rpi-image-generathor \
bash script to generate Debian image for Raspberry Pi
---

### Generate image
*Run:*
```
./rpi-image-generathor --help
```
to get usage info.

### Write image on SD card
For image write, you can use:
```
unxz rpi-image-armel.img.xz
dd if=rpi-image-armel.img of=/dev/mmcblk0 status=progress
```
or you can write `rpi-image-armel.img.xz` with software like \
Rufus (https://rufus.ie/en/) or Raspberry Imager (https://www.raspberrypi.com/software/)

#### Read-Only ramdisk Overlay
To enable Read-Only Ramdisk Overlay, use:
```
echo 1 > /boot/firmware/overlay.txt
```
To disable, use:
```
echo 0 > /boot/firmware/overlay.txt
```

---
**Image build tested on:** \
5.10.0-18-amd64 #1 SMP Debian 5.10.140-1 (2022-09-02) - Debian GNU/Linux 11 (bullseye) \
5.10.102.1-microsoft-standard-WSL2 #1 SMP Wed Mar 2 00:30:59 - Debian GNU/Linux bookworm/sid
