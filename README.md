# Device Tree for 9R (lemonades) for TWRP
## Disclaimer - Unofficial TWRP!
These are personal test builds of mine. In no way do I hold responsibility if it/you messes up your device.
Proceed at your own risk.

## Setup repo tool
Setup repo tool from here https://source.android.com/setup/develop#installing-repo

## Compile

Sync TWRP manifest:

```
repo init --depth=1 -u https://github.com/minimal-manifest-twrp/platform_manifest_twrp_aosp.git -b twrp-11

```

Make a directory named local_manifest under .repo, and create a new manifest file, for example lemonades.xml
and then paste the following

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<project path="device/oneplus/lemonades"
	name="schqiushui/android_device_oneplus_lemonades"
	remote="github"
	revision="android-11" />
</manifest>
```
You might need to pick few patches from gerrit.twrp.me to get some stuff working.

Sync the sources with

```
repo sync -j$(nproc --all)
```

To build, execute these commands in order

```
. build/envsetup.sh; export ALLOW_MISSING_DEPENDENCIES=true; export LC_ALL=C; lunch twrp_lemonades-eng; make -j$(nproc --all) adbd recoveryimage
```

To test it:

```
# To temporarily boot it
fastboot boot out/target/product/lemonades/recovery.img 

# Since Oneplus 9R has a separate recovery partition, you can flash the recovery with
fastboot flash recovery recovery.img
```

Kernel: https://github.com/LineageOS/android_kernel_oneplus_sm8250

##### Credits
- Blaster4385 for his tree
- theincognito for his tree
- bigbiff for decryption
- Systemad for original tree
- CaptainThrowback for original tree
- mauronofrio for original tree
- TWRP team
