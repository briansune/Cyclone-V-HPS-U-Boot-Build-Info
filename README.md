# Cyclone V HPS U-Boot Build Info

## How to Start

|Distro Tested|Distro Version|
|-|-|
|Ubuntu|20.04.6 LTS focal|

1) To start the build, first ensure cross-compile tools are installed.
2) Up to this markdown update, it is highly suggest to use the above distro as base.
3) It is ximilar but official Altera U-Boot is better on stability while official provides latest patches.
   + Clone via command "git clone https://github.com/u-boot/u-boot.git"
   + or
   + Clone via command "git clone https://github.com/altera-fpga/u-boot-socfpga"
4) After pulling, enter the directory
   + defines the cross-compile and architecture
   + setup the targeted platform via socfpga_cyclone5_defconfig
   + make prepare
   + make menuconfig if any modification is required
   + ensure the device-tree dts or dtsi is aligned with the board hardware
   + make -j (your-desire-cpu-#)
   + sudo dd if=u-boot-with-spl.sfp of=/dev/sdb1 bs=64k conv=fsync
   + cp u-boot.img SD Card boot parition
5) If things are running smooth powering up the board should read message on serial therminal.

## Issue discovered during build

+ For both official and upstream before 2025.07 the PL330 DMA reset is never released on any forms.
   + [patch](https://patchwork.ozlabs.org/project/uboot/patch/20250923181254.830-1-briansune@gmail.com/)
   + [documentation](https://patchwork.ozlabs.org/project/uboot/patch/20251008204103.1497-1-briansune@gmail.com/)
+ For upstream uboot 2025.07 2025.10 there is a mistake on "arch/arm/mach-socfpga/misc.c"


