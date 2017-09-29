Alz.ai's fork of FE fork of Linux kernel
============

### Toolchain
* Download toolchain from https://www.mediafire.com/folder/2nswfc4j82d9r/NanoPi-Duo#dzpfcupm0ssbx
	 * `mkdir -p /opt/FriendlyARM/toolchain`
	 * `tar xf arm-cortexa9-linux-gnueabihf-4.9.3.tar.xz -C /opt/FriendlyARM/toolchain/`

* Edit bashrc & add toolchain location PATH

	* `nano ~/.bashrc`
	* `export PATH=/opt/FriendlyARM/toolchain/4.9.3/bin:$PATH`
	* `export GCC_COLORS=auto`

### Building
* `touch .scmversion`
* `make sunxi_defconfig ARCH=arm CROSS_COMPILE=arm-linux-`
* `make zImage dtbs ARCH=arm CROSS_COMPILE=arm-linux-`

### Configuring
* `make menuconfig`

### Todo:
Implement DTS Patch for CX20921

### Potential issues:
*make menuconfig may fail if libncurses5-dev is not installed
	*run `sudo apt-get install libncurses5-dev` to fix