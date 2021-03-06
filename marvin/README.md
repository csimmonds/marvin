# Marvin: creating a minimal AOSP device

## Why Marvin?

Marvin demonstrates how to construct a minimal device on AOSP. It is based on
the Android Goldfish emulator [1] built for the x86_64 architecture. 

This version is based on AOSP 11

The name, Marvin, comes from the Hitchhikers Guide to the Galaxy, by Douglas Adams. Marvin
is a paranoid android, and he was manufactured by the Sirius Cybernetics
Corporation.

[1] Strictly speaking, Goldfish is the version of the emulator that is based on
QEMU 1. Goldfish was superseded in AOSP 5 by Rahchu, which is based on QEMU 2.
However, few of the code references were updated in AOSP to match this change,
so I will follow suit and call it Goldfish

## Preparation

Make sure that you have a system capable of building AOSP in a reasonable
amount of time, as described here...

[https://source.android.com/source/building.html](https://source.android.com/source/building.html).

...and here

[https://source.android.com/source/initializing.html](https://source.android.com/source/initializing.html)


## Download AOSP

Choose a directory for the AOSP source, e.g. $HOME/aosp:
```
$ mkdir ~/aosp && cd ~/aosp
```

Select the release of AOSP 11 you want, e.g. r32:
```
$ repo init -u https://android.googlesource.com/platform/manifest -b android-11.0.0_r32
$ repo sync -c
```
The total download is about 105 GB

If you don't care too much about the git history you can reduce the download by
about 48 GB by doing doing a shallow clone like this:
```
$ repo init --depth=1 -u https://android.googlesource.com/platform/manifest -b android-11.0.0_r32
```

Get Marvin:
```
$ cd ~/aosp/device
$ git clone https://github.com/csimmonds/marvin sirius -b android11

```

## Build AOSP

```
$ cd ~/aosp
$ source build/envsetup.sh
$ lunch marvin-eng
$ m
```
The command 'm' is a wrapper for 'make', with the additional benefit that it
will use all available CPU cores (see ~/aosp/build/soong/ui/build/config.go).

Even so, the build will take a few hours


## Run Marvin

Make sure that you have selected the product

```
$ cd ~/aosp
$ source build/envsetup.sh
$ lunch marvin-eng
```

Then launch the emulator
```
$ emulator
```


## Run Marvin in an AVD


An ADV is an Android Virtual Device which defines some parameters used by QEMU 



