# Cyclone V HPS U-Boot Build Info

## If this project is constructive, welcome to donate a drink to PayPal.

<img src="images/qrcode.png" style="height:20%; width:20%">

or 

paypal.me/briansune

## How to Start

|Distro Tested|Distro Version|
|-|-|
|Ubuntu|20.04.6 LTS focal|

1) To start the build, first ensure cross-compile tools are installed.
2) Up to this markdown update, it is highly suggest to use the above distro as base.
3) It is similar but official Altera U-Boot is better on stability while official provides latest patches.
   + Clone via command "git clone https://github.com/u-boot/u-boot.git"
   + or
   + Clone via command "git clone https://github.com/altera-fpga/u-boot-socfpga"
4) After pulling, enter the directory
   + defines the cross-compile and architecture
   + setup the targeted platform via socfpga_cyclone5_defconfig
   + Since newer build flow is introduce from official Altera U-Boot, cv_bsp_generator script is used to generate the board C files.
   + make prepare
   + make menuconfig if any modification is required
   + ensure the device-tree dts or dtsi is aligned with the board hardware
   + make -j (your-desire-cpu-#)
   + sudo dd if=u-boot-with-spl.sfp of=/dev/sdb1 bs=64k conv=fsync
   + cp u-boot.img SD Card boot parition
5) If things are running smooth powering up the board should read message on serial therminal.

[cv_bsp_generator](https://github.com/altera-fpga/u-boot-socfpga/tree/socfpga_v2025.07/arch/arm/mach-socfpga/cv_bsp_generator)

## Issue discovered during build

+ For both official and upstream before 2025.07 the PL330 DMA reset is never released on any forms.
   + [patch](https://patchwork.ozlabs.org/project/uboot/patch/20250923181254.830-1-briansune@gmail.com/)
   + [documentation](https://patchwork.ozlabs.org/project/uboot/patch/20251008204103.1497-1-briansune@gmail.com/)
+ For upstream uboot 2025.07 2025.10 there is a mistake on "arch/arm/mach-socfpga/misc.c"


