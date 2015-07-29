# WandBoard-Eth-Install
# [Eth(Embedded)](http://www.ethembedded.com) [Wandboard.org](http://www.wandboard.org/)/[Ethereum](https://www.ethereum.org/) Install Instructions

### Supported Boards:
- Wandboard Quad

### Materials Needed:
- Wandboard development board
- 64GB micro SD Card  
- Power Supply for Wandboard(5VDC 2A standard barrel connector)
- Ethernet cable (to connect to available, DHCP enabled, internet router)

##### Note: although 64GB is not immediately necessary, as the ethereum blockchain grows you will need the room to 		store it. (At least until SPV is available) Another strong suggestion is to use Class 10 SanDisk Ultra or Extreme models with higher R/W speeds

### Optional Materials:
- Micro HDMI->HDMI cable
- Monitor with HDMI input(or apropriate adapter)
- USB Keyboard

### Installation Method 
###### *Disclaimer* - If you will be formatting an SD card be aware that you will be deleting all information stored on said card.  Eth(Embedded) is *NOT*  responsible for any data loss that may occur during the format process.

1. Insert your FAT32 formatted SD card into your linux PC or Laptop. 
2. Download the Ubuntu 15.04lts image from http://www.wandboard.org/downloads:
  
  - Image link: http://www.wandboard.org/images/downloads/ubuntu-1504-lxde-wandboard-20150520.zip
  
2. Once you have downloaded the .img file we will need to extract it using [7zip](http://www.7-zip.org/), and then burn the image to our SD card using [WinDiskImager](http://sourceforge.net/projects/win32diskimager/) on Windows, or just use `tar` and `dd` on Linux following the how-to here: https://www.raspberrypi.org/documentation/installation/installing-images/linux.md
3. Safely remove and install SD card into a powered down Wandboard with ethernet cable connected between device and an internet enabled DHCP router.
4. Power on your Wandboard.
5. While the Wandboard is booting, we need to log in to our router and look at the dhcp client list to find the IP address assigned to our Wandboard device, alternately you can use one of my favorite mobile apps, [FING](https://play.google.com/store/apps/details?id=com.overlook.android.fing&hl=en), as long as your android phone is connected to the same network. We can then, using a linux cli or [putty](http://www.putty.org/), ssh[(instructions)](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-6-using-ssh/using-ssh-on-a-mac-or-linux) into the device with the following *default* credentials:

	- login : `wandboard`
	- password: `wandboard`

6. At this point lets take the opportunity to change the `wandboard` users password: 

	`passwd` and follow on screen instructions...
	
7. We also need to log off, and then log in as root to change the default root password:

	- login : `root`
	- password: `root`

	then...

	`passwd` and follow on screen instructions...

8. Next lets re-login as the `wandboard` user and expand partition #2 to utilize the entire SD Card: 

	`sudo fdisk /dev/mmcblk0`
	
	We can press `p` for print to see our current setup and give you a reference moving forward.
	
	Next we need to delete and then re-create partition #2 by selecting:
	
	-`d` - delete
	-`2` - partition to be deleted
	-`n` - create new partition
	-`p` - select partition type primary
	-`enter` - select default start block
	-`enter` - select default last block

9. Now lets download & unzip the installer scripts and choose eth-installer.sh OR geth-installer.sh:

	`wget https://github.com/EthEmbedded/Wandboard-Eth-Install/archive/v0.1.8.tar.gz`

	`tar -xvzf v0.1.8.tar.gz`
	
	`cd Wandboard-Eth-Install-0.1.8`

	`sudo chmod +x geth-installer.sh` OR `sudo chmod +x eth-installer.sh` 
	
9. Now lets run the install script for either `geth` or `eth`

	`./geth-installer.sh`
	
	OR
	
	`./eth-installer.sh`
	
	***NOTE*** - If a window pops up requesting you to restart services during the process, feel free to select yes.
	
10. Finally lets start the client:

	For `geth` :
	
	`cd ~/go-ethereum/build/bin`
	
	`./geth`
	
	For `eth`:
	
	`cd ~/cpp-ethereum/build/eth`
	
	`./eth`

####For more info regarding running cli clients please visit the following links:

For geth/go-ethereum visit: https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options

For eth/cpp-ethereum visit: https://github.com/ethereum/cpp-ethereum/wiki/Using-Ethereum-CLI-Client

####For more information regarding the Hardkernel Odroid Series of boards visit:

Main Homepage: http://www.hardkernel.com/main/main.php

####What now?

*To learn more about Ethereum.org get involved!*

A great place to start are the forums at https://forum.ethereum.org/

OR

Learn more about creating DApps by visiting https://dappsforbeginners.wordpress.com/

