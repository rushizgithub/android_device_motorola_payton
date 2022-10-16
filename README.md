# TWRP Device configuration for Motorola Moto X4 (payton)

Copyright 2018 - The OmniROM Project
Copyright 2022 - The TeamWin Recovery Project

For building TWRP for Motorola Moto X4 ONLY.

### Kernel Source
https://github.com/moto-SDM660/android_kernel_motorola_sdm660/tree/twrp-12.1

### Device specifications
=====================================

Basic   | Spec Sheet
-------:|:-------------------------
CPU     | Octa-core (8x2.21 GHz Cortex A53)
CHIPSET | Qualcomm SDM630 Snapdragon 630
GPU     | Adreno 508
Memory  | 3, 4, 6 GB
Shipped Android Version | 7.1.1 (Nougat)
Storage | 32, 64GB
Battery | 3000 mAh
Dimensions | 148.4 x 73.4 x 8 mm (5.84 x 2.89 x 0.31 in)
Display | 1080 x 1920 pixels, 5.2" LTPS IPS LCD 16:9 ratio (~424 ppi density)
Rear Camera 1 (main | 12 MP f/2.0 1.4-micron pixels and dual pixel autofocus
Rear Camera 2 (ultrawide) | 8 MP f/2.2 and fixed focus
Front Camera | 16 MP with flash and fixed focus

<p align="center">
<img height="600" src="https://i.imgur.com/pEEUbfS.png" title="Motorola Moto X4 (payton)"/>
</p>

## Compile

First repo init the twrp-12.1 tree:

```
mkdir ~/android/twrp-12.1
cd ~/android/twrp-12.1
repo init -u git://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-12.1
mkdir -p .repo/local_manifests
```

Then add to a local manifest (if you don't have .repo/local_manifest then make that directory and make a blank file and name it something like twrp.xml):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="osm0sis/twrp_abtemplate" path="bootable/recovery/installer" remote="github" revision="master"/>
  <project name="android_device_motorola_payton" path="device/motorola/payton" remote="TeamWin" revision="android-12.1"/>
</manifest>
```

Now you can sync your source:

```
repo sync
```

To automatically make the TWRP installer zip, you need to import this commit in the build/make path: https://gerrit.twrp.me/c/android_build/+/5445

Finally execute these:

```
. build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export LC_ALL=C
lunch twrp_payton-eng
make adbd bootimage
```
