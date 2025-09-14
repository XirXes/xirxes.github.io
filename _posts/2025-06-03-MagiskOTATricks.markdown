---
layout: post
title:  "OTA On Stock with Magisk"
---


Restore stock boot image, the current booted version of your OS, to the current slot. Use `adb shell` to run the following commands. Run the `getprop` command to check the slot you are on. Use that for the following commands.

```
getprop ro.boot.slot_suffix
> _a
su

source /data/adb/magisk/util_functions.sh
get_flags
find_block init_boot_a
> /dev/block/by-name/init_boot_a
flash_image /sdcard/boot/init_boot-810.img /dev/block/by-name/init_boot_a
```

DO NOT REBOOT, just install the OTA. I use Oxygen Updater and Local Update, but this method should work with the built in updater as well. On OnePlus this is the Extract step. INSTALL = REBOOT, wait a sec
First flash the updated boot image created by extracting the OTA and patching the image in the Magisk app. Flash the modified image to the other slot, oposite the earlier commands. 

Some devices may have a public repository of images, such as [this one for my OnePlus 12.](https://github.com/snowwolf725/OnePlus12-fw-repos/releases)

```
find_block init_boot_b
> /dev/block/sde66
flash_image /sdcard/Download/magisk_patched-27000_YT9ed.img /dev/block/sde66
```

Now, press the install button in the updater, rebooting the device, with root preinstalled on the newer version. 
This is pretty universal, OnePlus has a separate partition for the initram filesystem image, instead of the usual setup with the ramdisk packed into the boot.img. 

Note I gave both possible examples of output from `find_block`, the actual block device, or the alias in the by-name folder

It is possible to extract OTA images using `ota_extractor` from LineageOS' android_tools_extract-utils repo. Information on that is best from the source [here](https://wiki.lineageos.org/extracting_blobs_from_zips)

I extracted the OTA with my existing copy of the current version as the `input_dir` and the delta update to the newer version.
```
$LINPATH/prebuilts/extract-tools/linux-x86/bin/ota_extractor --payload payload.bin --input_dir ../../OP12NA-810/out
```
810 being the version I was on.
