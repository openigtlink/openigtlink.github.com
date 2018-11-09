---
layout: page
title: Tutorials > OpenIGTLink for Single-Board Computers
header: Pages
---
{% include JB/setup %}

##Introduction

A Single-Board Computer (SBC) is a small computer built on a single circuit board typically used as embedded computer  in hardware systems. Recently, hobby-oriented SBCs equipped with ARM-based processors have become popular and widely used for the hobby, educational, and research purposes. This page demonstrates how to develop and deploy an OpenIGTLink interface for ARM-based SBC using [BeagleBone Black Wireless](https://beagleboard.org/black-wireless) (BBB). The goal is to setup a cross-compile enviroment to compile and build the OpenIGTLink libary (and application that uses the library) on a PC, and then execute the binary on the BBB hardware. While it is possible to build the OpenIGTLink library on BBB, we recommend to compile on the PC because it would be a lot faster. 

##Prerequisite
1. A host Linux PC for development (Ubuntu 18.04 was used for testing)
2. [BeagleBone Black Wireless](https://beagleboard.org/black-wireless) (BBB)

##Connect BBB to Host PC
There are several ways to establish TCP/IP connection between BBB and the host PC, including Ethernet, WiFi, and USB. Please refer to [Getting Started page](https://beagleboard.org/getting-started).

##Setup Cross-Compile Environment
To build a binary file for BBB (ARM-based) on the host PC (Intel-based), we setup a cross-compile environment using [Linaro](https://www.linaro.org/). Linaro provides binary cross-compile packages for Linux environments. Linaro can be also bulit using a toolchain build scripts like [crosstool-NG](http://crosstool-ng.github.io/) if you cannot find the right binary for the OS of your host PC (includig macOS).

First, login to your BBB using SSH (assuming that the IP for BBB is 192.168.7.2):

    $ ssh -l debian 192.168.7.2
    
    Debian GNU/Linux 8
    
    BeagleBoard.org Debian Image 2016-11-06
    
    Support/FAQ: http://elinux.org/Beagleboard:BeagleBoneBlack_Debian
    
    default username:password is [debian:temppwd]
    
    debian@192.168.7.2's password: 
    Last login: Sun Nov  6 15:34:01 2016 from 192.168.7.1
    debian@beaglebone:~$ 

Then check the compile version of your BBB by:

    debian@beaglebone:~$ gcc -v
    Using built-in specs.
    COLLECT_GCC=gcc
    COLLECT_LTO_WRAPPER=/usr/lib/gcc/arm-linux-gnueabihf/4.9/lto-wrapper
    Target: arm-linux-gnueabihf
    Configured with: ../src/configure -v --with-pkgversion='Debian 4.9.2-10' --with-bugurl=file:///usr/share/doc/gcc-4.9/README.Bugs --enable-languages=c,c++,java,go,d,fortran,objc,obj-c++ --prefix=/usr --program-suffix=-4.9 --enable-shared --enable-linker-build-id --libexecdir=/usr/lib --without-included-gettext --enable-threads=posix --with-gxx-include-dir=/usr/include/c++/4.9 --libdir=/usr/lib --enable-nls --with-sysroot=/ --enable-clocale=gnu --enable-libstdcxx-debug --enable-libstdcxx-time=yes --enable-gnu-unique-object --disable-libitm --disable-libquadmath --enable-plugin --with-system-zlib --disable-browser-plugin --enable-java-awt=gtk --enable-gtk-cairo --with-java-home=/usr/lib/jvm/java-1.5.0-gcj-4.9-armhf/jre --enable-java-home --with-jvm-root-dir=/usr/lib/jvm/java-1.5.0-gcj-4.9-armhf --with-jvm-jar-dir=/usr/lib/jvm-exports/java-1.5.0-gcj-4.9-armhf --with-arch-directory=arm --with-ecj-jar=/usr/share/java/eclipse-ecj.jar --enable-objc-gc --enable-multiarch --disable-sjlj-exceptions --with-arch=armv7-a --with-fpu=vfpv3-d16 --with-float=hard --with-mode=thumb --enable-checking=release --build=arm-linux-gnueabihf --host=arm-linux-gnueabihf --target=arm-linux-gnueabihf
    Thread model: posix
    gcc version 4.9.2 (Debian 4.9.2-10) 
    debian@beaglebone:~$ 

In the above example, the compiler version is 4.9.2. Once you find out the compiler version, download the binary package from [the Linaro binary downlaod page](https://releases.linaro.org/components/toolchain/binaries/). Please make sure that the first two digits of the complier version on your BBB (4.9) matches the version number of the Linaro package. You can downlaod directly from the web browser, or using wget:

    $ wget -c https://releases.linaro.org/components/toolchain/binaries/4.9.4-2017.01/arm-linux-gnueabihf/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf.tar.xz

Finally, extract the files and copy them to the install folder:

    $ tar xf gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf.tar.xz
    $ mv gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf <install folder>

##Build the OpenIGTLink library
We will build the OpenIGTLink library for (1) the host PC and (2) BBB.

First, obtian the code from GitHub:

    $ git clone https://github.com/openigtlink/OpenIGTLink.git

Then create a build directory for the host, and build the library:

    $ cd <working directory>
    $ mkdir OpenIGTLink-build-x86
    $ cd OpenIGTLink-build-x86
    $ cmake -DBUILD_EXAMPLES=1 ../OpenIGTLink

Create a build directory for BBB:

    $ cd <working directory>
    $ mkdir OpenIGTLink-build-arm
    $ cd OpenIGTLink-build-arm

To run a cross-compile from CMake, you need to make a toolchain file. Create a text file with the following contents and save it as "toolchain.cmake" in the build folder. Make sure to replace <install folder> with the actual path you installed the cross compiler:

    set(CMAKE_SYSTEM_NAME Linux)
    set(CMAKE_SYSTEM_PROCESSOR arm)
    
    set(tools <install folder>/gcc-linaro-4.9.4-2017.01-x86_64_arm-linux-gnueabihf)
    set(CMAKE_C_COMPILER ${tools}/bin/arm-linux-gnueabihf-gcc)
    set(CMAKE_CXX_COMPILER ${tools}/bin/arm-linux-gnueabihf-g++)
    
    set(CMAKE_FIND_ROOT_PATH_MODE_PROGRAM NEVER)
    set(CMAKE_FIND_ROOT_PATH_MODE_LIBRARY ONLY)
    set(CMAKE_FIND_ROOT_PATH_MODE_INCLUDE ONLY)
    set(CMAKE_FIND_ROOT_PATH_MODE_PACKAGE ONLY)

Finally, build the binary for BBB using the following commands:

    $ cmake -DBUILD_EXAMPLES=1 -DCMAKE_TOOLCHAIN_FILE=toolchain.cmake ../OpenIGTLink

##Testing

Test the binaries by sending tracking data from the host PC to BBB.

Copy the binary file to BBB:

    $ cd <working directory>/OpenIGTLink-build-arm
    $ cd bin
    $ scp ReceiveServer debian@192.168.7.2:

Open a second terminal and login to BBB:

    $ ssh -l debian 192.168.7.2

Start the server:

    $ ./ReceiveServer 18944

Go back to the original terminal and start TrackerClient. Make sure to use the binary for the host:

    $ cd <working directory>/OpenIGTLink-build-x86
    $ cd bin
    $ ./TrackerClient 192.168.7.2 18944 10

You should see the received matrices on the second terminal, if the binaries are working.

##References

- https://www.digikey.com/eewiki/display/linuxonarm/BeagleBone+Black










