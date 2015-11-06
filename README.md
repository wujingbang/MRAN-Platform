# MRAN-Platform
A Multi-radio Ad-hoc Network Platform.

##Hardware
1. Intel Edison with Arduino kit.
	* https://software.intel.com/en-us/iot/library/edison-getting-started 
	* https://www.arduino.cc/en/ArduinoCertified/IntelEdison

1. RF4463F30 (si4463)
	* https://item.taobao.com/item.htm?spm=a230r.1.14.1.DwnEJR&id=37095299434&ns=1&abbucket=17#detail

1. RF4463F30 to Edison converter board
	* Documents/rf4463f30-to-edison-pcb

1. xiaomi 10000mAh power bank
	* http://www.mi.com/dianyuan10000/

## System compile for Edison
1. https://github.com/xyongcn/vanet-radio#build-an-intel-edison-image
	
2. Patch the edison kernel with 0001-default-chan-for-802154.patch (for yocto release 2.0), rebuild the edison-image.
	1. clean the linux build.
		* bitbake -c cleansstate linux-yocto
	2. patch:
		* https://github.com/xyongcn/vanet-radio/blob/master/kernel_driver/0001-default-chan-for-802154.patch
		* Move the patch file to the edison-src/device-software/meta-edison/recipes-kernel/linux/files
		* vi edison-src/device-software/meta-edison/recipes-kernel/linux/linux-yocto_3.10.bbappend
		* Add one line at the bottom:
			* SRC_URI += "file://0001-default-chan-for-802154.patch"
3. Replace the defconfig for kernel.
	1. https://github.com/xyongcn/vanet-radio/blob/master/kernel_driver/defconfig
	2. mv defconfig edison-src/device-software/meta-edison/recipes-kernel/linux/files
3. Rebuild:
	* bitbake edison-image

4. Flash the edison.

## Kernel driver for rf4463f30
https://github.com/xyongcn/vanet-radio/tree/master/kernel_driver

## Access and Debug
1. Bluetooth adb shell for edison:
	* https://github.com/xyongcn/bt-adb-shell
	* Note: There has a unsolved problem that the bt-adb-shell cannot transfer files.

1. Use the wifi & ssh to transfer files.
	* https://software.intel.com/en-us/get-started-edison-linux-step5
