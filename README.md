# pogoplug-v3-oxnas-debian-squeeze

ArchLinux ARM ("ALARM") switch to Debian Squeeze

Just found this Pogoplug in one of my cabinets. It was still able to boot up, but since Arch Linux do not maintain for old devices, installing new updates was completely broken my OS. After a lot of research, switching to debian squeeze is a safe way that makes the pogoplug v3 usable again, as most other methods required a ttl cable and flash uboot.

This image was made by myself and followed the guideline from howtoforge.

- Changed to Debian Archive source and disabled PGP check, so you can install packages.

## Login / Password

root / rootroot

## How to Use

### Requirements

- You previously installed Arch Linux ARM ("ALARM") on your Pogoplug V3
- USB Drive 1: Ubuntu Live USB (You don't need this if you have Linux PC or Raspberry Pi)
- USB Drive 2: Use as Pogoplug drive

### Windows

You need Ubuntu Live USB to do that. You need one more USB drive:

1. Download Rufus (https://rufus.ie)
1. Follow this guide to prepare a Ubuntu Live USB (https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview)
1. Boot into Ubuntu
1. Go to Linux Section and continue the steps

### Linux

1. Get a empty USB drive.
1. Do everything in root.
    ```bash
    `sudo -i` 
    # or 
    su
    ```
1. Check the USB drive path, the path should looks like `/dev/sdb`.
    ```bash
    `fdisk -l`
    ```
1. Erase your USB drive, it takes a few minutes.
    ```bash
    dd if=/dev/zero of=/dev/<your name e.g. sdb>  bs=512 count=1024
    fdisk /dev/<your name e.g. sdb> 
    ```
1. Following this steps to create a partition:
    ```bash
    Command (m for help): n
    Select (default p): p
    Partition number (1-4, default 1): 1
    Command (m for help): w
   ```
1. Format your partition into a ext3 partition. ⚠️⚠️ Don't use wrong name, it should be like `/dev/sdb1` with a number 1 at the end.
    ```bash
    mkfs.ext3 -m00 /dev/<your name e.g. sdb1> 
    ```
1. Double check if your USB drive is in EXT3 partition.
    ```bash
    lsblk -f
    ```
1. Mount your USB drive.
    ```bash
    mkdir /mnt/pogostick
    mount /dev/<your name e.g. sdb1> /mnt/pogostick
    ```
1. Download the image.
    ```bash
    wget https://github.com/louislam/pogoplug-v3-oxnas-debian-squeeze/releases/download/1.0/Pogoplug_V3_Oxnas_Debian_Squeeze_20210831.tgz
    ```
1. Decompress all files to the root of your empty USB drive .
    ```bash
    tar -xvzf Pogoplug_V3_Oxnas_Debian_Squeeze_20210831.tgz -C /mnt/pogostick
    ```
1. View the /mnt/pogostick folder, you should see all the files.   
    ```bash
        root@louis-pi:/mnt/pogostick# ls -l
        total 107107
        drwxr-xr-x  2 root root      4096 Jan  1  2008 bin
        drwxr-xr-x  2 root root      4096 Jul 14  2014 boot
        drwxr-xr-x  3 root root      4096 Jan  1  2015 dev
        drwxr-xr-x 47 root root      4096 Jan  1  1970 etc
        drwxr-xr-x  2 root root      4096 Jul 14  2014 home
        drwxr-xr-x 10 root root      4096 Jan  1  1970 lib
        drwx------  2 root root     16384 Jul 20 17:28 lost+found
        drwxr-xr-x  2 root root      4096 Aug 26  2021 media
        drwxr-xr-x  2 root root      4096 Jul 14  2014 mnt
        drwxr-xr-x  2 root root      4096 Aug 26  2021 opt
        drwxr-xr-x  2 root root      4096 Jul 14  2014 proc
        drwx------  3 root root      4096 Aug 26  2021 root
        drwxr-xr-x  2 root root      4096 Aug 26  2021 sbin
        drwxr-xr-x  2 root root      4096 Jul 21  2010 selinux
        drwxr-xr-x  2 root root      4096 Aug 26  2021 srv
        drwxr-xr-x  2 root root      4096 Mar 28  2012 sys
        drwxrwxrwt  2 root root      4096 Aug 26  2021 tmp
        drwxr-xr-x 10 root root      4096 Aug 26  2021 usr
        drwxr-xr-x 13 root root      4096 Aug 26  2021 var
    ```
1. Edit `/mnt/usb/etc/network/interfaces` and change to your poloplug mac address (It should be under your pogoplug).
    ```bash
    # Edit the file using `nano`
    nano /mnt/usb/etc/network/interfaces
    # Press Ctrl + O to save
    ```
1. Unmount your USB drive.
    ```bash
    umount -l /mnt/pogostick
    ```
1. Remove the USB drive and plug it into your pogoplug.
1. Power on your pogoplug.
2. Wait for 5 minutes until the led light is solid green. You can now try to ssh to your pogoplug.

![image](https://github.com/louislam/pogoplug-v3-oxnas-debian-squeeze/assets/1336778/d799e725-7807-40c3-8c44-ecefdadb5280)


Reference:
https://www.howtoforge.com/installing-debian-squeeze-on-pogoplug-v3-oxnas-cleanly

## Install Software

You can install software by using `apt-get`, of course, there is no `apt`.

`apt-get install curl`


### Install PHP 5.3.3

```bash
apt-get install php5
php -v
```
