---
layout: page
title: Tutorials > ROS-IGTL-Bridge for Single-Board Computers
header: Pages
---
{% include JB/setup %}

Introduction
------------

The goal of this tutorial is to learn how to integrate a robotic system with medical image computing software using OpenIGTLink. Specifically, we will learn how to setup a [Robot Operating System](http://www.ros.org/) (ROS) and ROS-IGTL-Bridge on a single-board computer (SBC), and connect it to 3D Slicer running on a host computer. In this tutorial, we will use BeagleBone Black Wireless as an example of SBC, but any other SBC, such as Raspburry Pi could work in a similar manner.


Prerequisite
------------

* Hardware

1. A host computer for running 3D Slicer (macOS Sierra was used for testing)
2. [BeagleBone Black Wireless](https://beagleboard.org/black-wireless) (BBB)
3. microSD card 8GB or 16GB
4. SD card reader for the host computer

* Softwre packages
1. [3D Slicer](https://www.slicer.org) - Version 4.10
2. [Ubuntu Linux for Beagle Board](https://elinux.org/BeagleBoardUbuntu) - Version 18.04
3. [Robot Operating System](http://www.ros.org/) - Melodic Morenia


Create Ubuntu 18.04 bootable SD
-------------------------------

We will create a SD card with Ubuntu 18.04. Although a BBB comes with pre-installed Debian Linux, no binary package of ROS is available for Debian Linux on BBB. You can still build ROS for BBB, it is not straightforward because of the limited onboard storage (eMMC). The SD will also expand the storage size and will make it easier to install additional packages.

Binary images of Ubuntu 18.04 is available at [elinux.org](https://elinux.org/BeagleBoardUbuntu). We will follow the instruction for "raw microSD image":

Download the OS image and verify (for a Linux host):

  $ wget https://rcn-ee.com/rootfs/2018-09-11/elinux/ubuntu-18.04.1-console-armhf-2018-09-11.tar.xz
  $ sha256sum bone-ubuntu-18.04.1-console-armhf-2018-09-11-2gb* 39a4a24962e5241b7e0cb5b249f8dfddaa43b122d3826bcd923aa541321fb125  bone-ubuntu-18.04.1-console-armhf-2018-09-11-2gb.img.xz

If you use macOS, the image can be validated with 'shasum' instead of 'sha256sum':

  $ shasum -a 256 bone-ubuntu-18.04.1-console-armhf-2018-09-11-2gb.img.xz 39a4a24962e5241b7e0cb5b249f8dfddaa43b122d3826bcd923aa541321fb125  bone-ubuntu-18.04.1-console-armhf-2018-09-11-2gb.img.xz

Before writing the SD image to the media, check the device name. On Linux, you can check available disks before and after connecting the SD card:

  $ lsblk
  
  NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
  sda      8:0    0 465.8G  0 disk 
  ├─sda1   8:1    0 195.3G  0 part 
  ├─sda2   8:2    0     4G  0 part [SWAP]
  └─sda3   8:3    0 266.5G  0 part /
  sdb      8:16   0 465.8G  0 disk 
  └─sdb1   8:17   0 460.8G  0 part /home
  sr0     11:0    1  1024M  0 rom  

In Mac, run the following command after connecting the SD card:

  $diskutil list
  /dev/disk0 (internal):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:      GUID_partition_scheme                         1.0 TB     disk0
     1:                        EFI EFI                     314.6 MB   disk0s1
     2:          Apple_CoreStorage Macintosh HD            999.6 GB   disk0s2
     3:                 Apple_Boot Recovery HD             650.0 MB   disk0s3
  
  /dev/disk1 (internal, virtual):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:                  Apple_HFS Macintosh HD           +999.2 GB   disk1
                                   Logical Volume on disk0s2
                                   DFB2D908-FAE0-4DA1-9F8F-557F7F7B430D
                                   Unlocked Encrypted
  
  /dev/disk2 (external, physical):
     #:                       TYPE NAME                    SIZE       IDENTIFIER
     0:     FDisk_partition_scheme                        *15.9 GB    disk2
     1:             Windows_FAT_32 NO NAME                 15.9 GB    disk2s1

In this case, /dev/disk2 is the SD card. On the Mac, you may need to unmount the disk before writing the disk image to the SD card:

  $ diskutil unmountDisk /dev/disk2
  Unmount of all volumes on disk2 was successful

Then write the SD card image with 'dd' command

  $ xzcat bone-ubuntu-18.04.1-console-armhf-2018-09-11-2gb.img.xz | sudo dd of=/dev/disk2
  3481600+0 records in
  3481600+0 records out
  1782579200 bytes transferred in 689.521240 secs (2585242 bytes/sec)


Boot from the SD card
---------------------

In the following sections, we will work on the BBB from the host computer through the TCP/IP connection over the USB cable. You may need to install [a driver for network-over-USB](https://beagleboard.org/getting-started). 

Insert the SD card to the slot on the BBB, and connect the BBB and the host computer using a USB cable. Once the booting process is completed, you will be able to login to the BBB from the terminal on the host computer:

  $ ssh -X ubuntu@192.168.7.2
  ubuntu@192.168.7.2's password: 
  Warning: untrusted X11 forwarding setup failed: xauth key data not generated
  Last login: Tue Sep 11 20:20:52 2018 from 192.168.7.1

The default password is "temppwd". Once you log into the system, make sure that the system has an internet connection. If you want to connect to a WiFi network, please follow [How to setup WIFI from a Linux console](sbc-wifi).

Check the disk space on the system: 

  ubuntu@arm:~$ df
  Filesystem     1K-blocks    Used Available Use% Mounted on
  udev              219152       0    219152   0% /dev
  tmpfs              49580    3660     45920   8% /run
  /dev/mmcblk0p1   1676616 1047448    525952  67% /
  tmpfs             247880       0    247880   0% /dev/shm
  tmpfs               5120       4      5116   1% /run/lock
  tmpfs             247880       0    247880   0% /sys/fs/cgroup
  tmpfs              49576       0     49576   0% /run/user/1000


The downloaded disk image is designed for a media size of 2GB, and the sytem already occupies 67% of the space. However, if you have a SD card larger than 2GB, you can re-allocate the partition by the following command:

  ubuntu@arm:/opt/scripts/tools$ cd /opt/scripts/tools
  
  ubuntu@arm:/opt/scripts/tools$ git pull
  remote: Enumerating objects: 71, done.
  remote: Counting objects: 100% (71/71), done.
  remote: Compressing objects: 100% (27/27), done.
  remote: Total 63 (delta 43), reused 56 (delta 36), pack-reused 0
  Unpacking objects: 100% (63/63), done.
  From https://github.com/RobertCNelson/boot-scripts
     0aa8fd0..e9bcff2  master     -> origin/master
  Updating 0aa8fd0..e9bcff2
  Fast-forward
   boot/am335x_evm.sh            | 32 ++++++++++++++++++++++----------
   boot/beagle_x15.sh            |  5 +++++
   boot/omap3_beagle.sh          |  5 +++++
   network/doc-debian-setup.md   | 11 +++++++++++
   network/usb_linux_usb0_ics.sh | 14 ++++++++++++++
   network/usb_linux_usb1_ics.sh | 14 ++++++++++++++
   network/usb_mac_ics.sh        | 15 +++++++++++++++
   network/usb_windows_ics.sh    | 15 +++++++++++++++
   tools/update_kernel.sh        | 41 +++++++++++++++++++----------------------
   tools/version.sh              | 11 +++++++++++
   10 files changed, 131 insertions(+), 32 deletions(-)
   create mode 100644 network/doc-debian-setup.md
   create mode 100755 network/usb_linux_usb0_ics.sh
   create mode 100755 network/usb_linux_usb1_ics.sh
   create mode 100755 network/usb_mac_ics.sh
   create mode 100755 network/usb_windows_ics.sh

  ubuntu@arm:/opt/scripts/tools$ sudo ./grow_partition.sh 
  [sudo] password for ubuntu: 
  Media: [/dev/mmcblk0]
  sfdisk: 2.26.x or greater
  Disk /dev/mmcblk0: 14.9 GiB, 15931539456 bytes, 31116288 sectors
  Units: sectors of 1 * 512 = 512 bytes
  Sector size (logical/physical): 512 bytes / 512 bytes
  I/O size (minimum/optimal): 512 bytes / 512 bytes
  Disklabel type: dos
  Disk identifier: 0x6ae17082
  
  Old situation:
  
  Device         Boot Start     End Sectors  Size Id Type
  /dev/mmcblk0p1 *     8192 3481599 3473408  1.7G 83 Linux
  
  >>> Created a new DOS disklabel with disk identifier 0xaec33366.
  /dev/mmcblk0p1: Created a new partition 1 of type 'Linux' and of size 14.9 GiB.
  Partition #1 contains a ext4 signature.
  /dev/mmcblk0p2: Done.
  
  New situation:
  Disklabel type: dos
  Disk identifier: 0xaec33366
  
  Device         Boot Start      End  Sectors  Size Id Type
  /dev/mmcblk0p1 *     8192 31116287 31108096 14.9G 83 Linux
  
  The partition table has been altered.
  Calling ioctl() to re-read partition table.
  Re-reading the partition table failed.: Device or resource busy
  The kernel still uses the old table. The new table will be used at the next reboot or after you run partprobe(8) or kpartx(8).
  Syncing disks.
  reboot

  ubuntu@arm:/opt/scripts/tools$ sudo reboot
  Connection to 192.168.7.2 closed by remote host.
  Connection to 192.168.7.2 closed.

The last command 'reboot' will disconnect your SSH connection and reboot the BBB. Once it is rebooted, login with the same IP, username, and password.

  $ ssh -X ubuntu@192.168.7.2
  ubuntu@192.168.7.2's password: 
  Warning: untrusted X11 forwarding setup failed: xauth key data not generated
  Last login: Tue Sep 11 20:20:52 2018 from 192.168.7.1

To confirm the disk size, run the 'df' command again:

  ubuntu@arm:~$ df
  Filesystem     1K-blocks    Used Available Use% Mounted on
  udev              219012       0    219012   0% /dev
  tmpfs              49580    3636     45944   8% /run
  /dev/mmcblk0p1  15289388 1057108  13580320   8% /
  tmpfs             247880       0    247880   0% /dev/shm
  tmpfs               5120       4      5116   1% /run/lock
  tmpfs             247880       0    247880   0% /sys/fs/cgroup
  tmpfs              49576       0     49576   0% /run/user/1000


Install ROS Melodic Morenia
---------------------------

The next step is to install ROS Melodic Morenia (the latest long term support (LTS) as of November 2018). Please follow the installtion instruction available at [wiki.ros.org](http://wiki.ros.org/melodic/Installation/Ubuntu) on the BBB's console.


Install and test ROS-IGTL-Bridge
--------------------------------

Once the ROS environment has been set up, follow the README file in [the ROS-IGTL-Bridge package](https://github.com/openigtlink/ROS-IGTL-Bridge).





















