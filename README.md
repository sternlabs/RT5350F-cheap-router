# RT5350F-cheap-router

## Building OpenWrt

Download the snapshot Image Generator.

    wget https://downloads.openwrt.org/snapshots/trunk/ramips/generic/OpenWrt-ImageBuilder-ramips_rt305x-for-linux-x86_64.tar.bz2
    tar xjf OpenWrt-ImageBuilder-ramips_rt305x-for-linux-x86_64
    cd OpenWrt-ImageBuilder-ramips_rt305x-for-linux-x86_64

Build the image. You can add optional packages using the `PACKAGES=` variable.

    make image PROFILE="A5-V11" PACKAGES="iptables-mod-tee"

The command above adds `iptables-mod-tee` so we can TEE packets from iptables.

You will find the generated image inside `bin/ramips`.

## Installation

Point your browser to the default gateway given by the router (e.g. http://192.168.100.1). You can change the language to English in the web interface.
Find the firmware upgrade page and upload the `openwrt-ramips-rt305x-a5-v11-squashfs-factory.bin`. After flashing the router will reboot.

## Configuration

Access the router via telnet

    telnet 192.168.1.1

Set a root password, which will disable telnet and enable ssh

    passwd

## Upgrading OpenWrt

After building your image copy it to the `/tmp` folder. **Important:** We will use the `openwrt-ramips-rt305x-a5-v11-squashfs-sysupgrade.bin` file.

    scp bin/ramips/openwrt-ramips-rt305x-a5-v11-squashfs-sysupgrade.bin root@192.168.1.1:/tmp

Log into the router and use the `sysupgrade` utility.

	ssh root@192.168.1.1
	cd /tmp
	sysupgrade -v openwrt-ramips-rt305x-a5-v11-squashfs-sysupgrade.bin

Don't worry, system config files are saved by default.

## Images

<img src="https://farm6.staticflickr.com/5483/12224520464_90c79d648b_m.jpg" width="240" height="80" alt="MPR-A5 Mini AP Wireless Router">

## References

* http://my-embedded.blogspot.de/2013/12/mini-4g-router-rt5350f.html
* http://wiki.openwrt.org/toh/unbranded/a5-v11
* http://www.digitalinferno.com/wiki/Wiki.jsp?page=Mini3G4GUSBRouterOpenWrtExternalUSB
