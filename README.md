# DragonBoard 410c Gadget Snap

This repository contains the official Ubuntu Core gadget snap for the
DragonBoard 410c.

## Gadget Snaps

Gadget snaps are a special type of snaps that contain device specific support
code and data. You can read more about them in the snapd wiki
https://github.com/snapcore/snapd/wiki/Gadget-snap

## Reporting Issues

Please report all issues on the Launchpad project page
https://bugs.launchpad.net/snap-dragonboard/+filebug

We use Launchpad to track issues as this allows us to coordinate multiple
projects better than what is available with Github issues.

## Building

To build the gadget snap locally please use `snapcraft --target-arch=arm64`.

## Launchpad Mirror and Automatic Builds.

All commits from the master branch of https://github.com/snapcore/dragonboard
are automatically mirrored by Launchpad to the
https://launchpad.net/snap-dragonboard project.

The master branch is automatically built from the launchpad mirror and
published into the snap store to the edge channel.

You can find build history and other controls here:
https://code.launchpad.net/~canonical-foundations/+snap/dragonboard

## Old content

This used to be in the old README file, it will be phased out over time

```
uboot.env is created from uboot.env.in via:
$ mkenvimage -r -s 131072  -o uboot.env uboot.env.in
```

## Building u-boot:
```
$ git clone git://git.denx.de/u-boot.git -b v2017.05
$ git apply sd_u-boot.patch
$ make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- dragonboard410c_defconfig
$ make ARCH=arm CROSS_COMPILE=aarch64-linux-gnu- -j4
```
repack u-boot to android boot.img format
use tool from: git://codeaurora.org/quic/kernel/skales
```
$ ./dtbTool -o u-boot-dt.img -s 2048 arch/arm/dts/
$ touch u-boot-ramdisk.img
$ ./mkbootimg --kernel=u-boot.bin --output=u-boot.img --dt=u-boot-dt.img --pagesize 2048 --base 0x80000000 --ramdisk=u-boot-ramdisk.img --cmdline=""
```

## Build lk:
```
$ git clone http://git.linaro.org/landing-teams/working/qualcomm/lk.git -b dragonboard410c-LA.BR.1.2.7-03810-8x16.0-linaro1
toolchain: $ git clone  git://codeaurora.org/platform/prebuilts/gcc/linux-x86/arm/arm-eabi-4.8.git -b LA.BR.1.1.3.c4-01000-8x16.0
$ make -j4 msm8916 EMMC_BOOT=1 TOOLCHAIN_PREFIX=/home/ubuntu/snappy-devices/arm-eabi-4.8/bin/arm-eabi-
```


## Build fastboot partition table blob
```
$ git clone https://git.linaro.org/landing-teams/working/qualcomm/db-boot-tools.git
$ sudo ./mksdcard -g -o sd.img -p emmc-partitions.txt; sudo sgdisk -bgpt.bin sd.img; ./mkgpt -i gpt.bin -o gpt_both0.bin
```

## Repartition emmc with fastboot
boot board to fastboot mode
```
$ prebuilt/flashall
```
