# pogoplug-v3-oxnas-debian-squeeze

ArchLinux ARM ("ALARM") switch to Debian Squeeze

Just found this Pogoplug in one of my cabinets. It was still able to boot up, but since Arch Linux do not maintain for old devices, installing new updates was completely broken my OS. After a lot of research, switching to debian squeeze is a safe way that makes the pogoplug v3 usable again, as most other methods required a ttl cable and flash uboot.

This image was made by myself and followed the guide line from howtoforge. 

- Changed to Debian Archive source and disabled PGP check, so you can install packages.

## Login / Password

root / rootroot

## How to Use

1. Better in Linux environment, you can use Ubuntu Live CD or USB Drive
1. Get a empty USB drive
2. should be in MBR and format a EXT3 partition
3. Download https://github.com/louislam/pogoplug-v3-oxnas-debian-squeeze/releases/download/1.0/Pogoplug_V3_Oxnas_Debian_Squeeze_20210831.tgz
4. Do everything in root `sudo -i` 
6. Unzip all files to the root of your empty USB drive
7. Go to `./etc/network/interfaces` and change to your poloplug mac address
8. Done, you can try to boot it.

Reference:
https://www.howtoforge.com/installing-debian-squeeze-on-pogoplug-v3-oxnas-cleanly
