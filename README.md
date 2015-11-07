webos-ports-setup
=================

Helper scripts for setting up an webOS ports development environment. Instructions for building for Raspberry Pi:

#### Setup build environment

Before you can build, you will need some tools. If you try to build without them, bitbake will fail a sanity check and tell you about what's missing, but not really how to get the missing pieces.

If your distribution is Ubuntu, you need to be running the bash shell. You can be sure you are running this shell by entering the following command and selecting "No" at the prompt:

```
  $ sudo dpkg-reconfigure dash
```

The essential and graphical support packages you need for a supported Ubuntu or Debian distribution are shown in the following command:

```
  $ sudo apt-get install gawk wget git-core diffstat unzip texinfo \
  build-essential chrpath libsdl1.2-dev xterm
```

For other Linux distributions please have a look at [the Yocto Project Quick Start guide](https://www.yoctoproject.org/docs/1.5/yocto-project-qs/yocto-project-qs.html).

```
  $ cd into-your-build-directory
  $ mkdir webos-ports-rpi && cd webos-ports-rpi
  $ wget https://raw.github.com/Andolamin/webos-ports-setup/alan/raspberrypi/Makefile
  $ make setup-webos-ports
```

#### Building

Make sure you're _not_ root, as the build will fail. If you SU in the middle, don't forget to set up env afresh (. setup-env)

To configure to build (notice '.' which is actually bash 'source' command):

```
  $ cd into-your-build-directory/webos-ports-rpi/webos-ports
  $ . setup-env
```

Then, build:

```
  $ MACHINE=raspberrypi2 bb luneos-dev-image
```

#### Flashing the image

To flash the image to your SD card, first you need to find which device is the correct one. Run `lsblk` or `df -h` and find the one that looks like your card. For example, mine is /dev/sdd, but it will likely differ for you.

Unmount your drive

```
sudo umount /dev/sdd*
```

Flash the image. I used luneos-image and raspberrypi2 so the following represents that. You might have to update your image path accordingly

```
sudo dd if=tmp-glibc/deploy/images/raspberrypi2/luneos-image-raspberrypi2.rpi-sdimg of=/dev/sdd
```
