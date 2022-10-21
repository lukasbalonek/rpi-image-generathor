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

### Grow system partition to fit SD card capacity
Install packages for `resize2fs` and `growpart`:
```
apt -yq install e2fsprogs cloud-guest-utils
```
Grow partition:
```
growpart /dev/mmcblk0 2
```
Grow filesystem:
```
resize2fs /dev/mmcblk0p2
```

### Good to know

#### initramfs-update
To update init ramdisk, use:
```
update-initramfs-overlay
```
instead of:
```
update-initramfs -u
```
because if you've got mounted `overlay on /`, `update-initramfs` will set `root=overlay`
in `/boot/firmware/cmdline.txt` and your system will not boot until you change it to `root=/dev/mmcblk0p2`

#### Read-Only ramdisk Overlay
To enable Read-Only Ramdisk Overlay, use:
```
echo 1 > /boot/overlay.txt
```
To disable, use:
```
echo 0 > /boot/overlay.txt
```
