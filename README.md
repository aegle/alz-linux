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
### Requirements
* `sudo apt-get install python device-tree-compiler build-essential libncurses5-dev`

### Building
* `touch .scmversion`
* `make sunxi_defconfig ARCH=arm CROSS_COMPILE=arm-linux-`
* Configuring
	* `make menuconfig ARCH=arm CROSS_COMPILE=arm-linux-`
* All in one command:
	* `make zImage dtbs modules modules_install INSTALL_MOD_PATH=~/h3-linux/built_modules ARCH=arm CROSS_COMPILE=arm-linux-`
* Or individually:
	* `make zImage dtbs ARCH=arm CROSS_COMPILE=arm-linux-`
	* `make modules ARCH=arm CROSS_COMPILE=arm-linux-`
	* `make modules_install INSTALL_MOD_PATH=~/h3-linux/MODULES ARCH=arm CROSS_COMPILE=arm-linux-`

### U-boot
* `cd ~`
* `sudo apt-get install python device-tree-compiler`
* `git clone https://github.com/friendlyarm/u-boot.git`
* `cd u-boot`
* `git checkout sunxi-v2017.x`
* `make nanopi_m1_plus_defconfig ARCH=arm CROSS_COMPILE=arm-linux-`
* `make ARCH=arm CROSS_COMPILE=arm-linux-`
* `sudo dd if=u-boot-sunxi-with-spl.bin of=/dev/mmcblk0 bs=1024 seek=8`

### Preparing a SD Card (Using dibs image) where /k/ is /yourusername/
* `cd ~/h3-linux/arch/arm/boot/`
* `sudo cp -R zImage /run/media/k/boot/`
* `sudo cp -R Image /run/media/k/boot/`
* `cd ~/h3-linux/arch/arm/boot/dts`
* `sudo cp -R sun8i-h3-nanopi-neo-air.dtb /run/media/k/boot/`
* `cd ~/h3-linux/MODULES/`
* `sudo cp -R lib/ /run/media/k/rootfs/`
* `cd ~/dibs/`
* `fakeroot sudo tar -xzf alz-duo.tar.gz -C /run/media/k/rootfs/`

### Todo:

### Notes:
* run `speaker-test -c 2 -r 44100 -D hw:1,0` to test speakers
*`fakeroot sudo tar -xzpf alz-duo.tar.gz -C /run/media/k/rootfs/` may be better, but has sometimes caused issues. Should investigate
