# mica-feed
This feeds holds the SDK wifi driver and the config/meta package for the MiCa7688

# Build the firmware from sources

This section describes how to build the firmware for MiCa7688 from source codes.


### Host environment
The following operations are performed under a Debian Stretch environment. For a Windows or a Mac OS X host computer, you can install a VM for having the same environment:



### Steps
In the Debian system, open the *Terminal* application and type the following commands:

1. Install prerequisite packages for building the firmware:
    ```
    $ sudo apt-get install git g++ make libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip wget python xz-utils
    ```

2. Download OpenWrt CC source codes:
    ```
    $ git clone git://git.openwrt.org/15.05/openwrt.git
    ```
    
3. Prepare the default configuration file for feeds:
    ```
    $ cd openwrt
    $ cp feeds.conf.default feeds.conf
    ```
    
4. Add the MiCa7688 feed:
    
    ```
    $ echo src-git mica https://github.com/emavap/MiCa-feed.git >> feeds.conf
    ```
5. Update the feed information of all available packages for building the firmware:
    
    ```
    $ ./scripts/feeds update
    ```
6. Install all packages:
    
    ```
    $ ./scripts/feeds install -a
    ```
7. Prepare the kernel configuration to inform OpenWrt that we want to build an firmware for LinkIt Smart 7688:
    
    ```
    $ make menuconfig
    ```
    * Select the options as below:
        * Target System: `Ralink RT288x/RT3xxx`
        * Subtarget: `MT7688 based boards`
        * Target Profile: `MiCa7688`
    * Save and exit (**use the deafult config file name without changing it**)
8. Start the compilation process:
    
    ```
    $ make V=99
    ```
9. After the build process completes, the resulted firmware file will be under `bin/ramips/openwrt-ramips-mt7688-MiCa7688-squashfs-sysupgrade.bin`. Depending on the H/W resources of the host environment, the build process may **take more than 2 hours**.

10. You can use this file to do the firmware upgrade through the Web UI. Or rename it to `wrt7688.img` for upgrading through a USB drive.

