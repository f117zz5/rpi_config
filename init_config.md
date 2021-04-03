## Create the SD card under Linux
The main article is [here](https://www.raspberrypi.org/documentation/installation/installing-images/linux.md). 

Run 
```
lsblk -p
```
in order to identify the card. Then download the image, verify the SHA-256 and burn it to the card like:
```
dd bs=4M if=2020-02-13-raspbian-buster-lite.img of=/dev/mmcblk0 conv=fsync
```

## Enable USB SSD boot
Main article [here](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bootmodes/msd.md)

```
echo program_usb_boot_mode=1 | sudo tee -a /boot/config.txt
```

After reboot check it with 
```
vcgencmd otp_dump | grep 17:
```

The output should be *3020000a*.

## Create new user with sudo privileges 

Original article here: [link](https://raspi.tv/2012/how-to-create-a-new-user-on-raspberry-pi) and [here](https://www.raspberrypi.org/documentation/linux/usage/users.md) from raspberrypi.org
```
sudo adduser bob
sudo adduser bob sudo
```

Another option from [this](https://www.raspberrypi.org/documentation/configuration/security.md) page:
```
sudo usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,input,netdev,gpio,i2c,spi bob
```
Disable the swap partition, will be reenabled at reboot:
```
sudo swapoff -a
```
Original article [here](https://www.raspberrypi.org/forums/viewtopic.php?t=244130)

Increase the size of the swap file, original article [here](https://nebl.io/neblio-university/enabling-increasing-raspberry-pi-swap/)

Temporary stop the swap file
```
sudo dphys-swapfile swapoff  
```
Edit as root */etc/dphys-swapfile* and set *CONF_SWAPSIZE=1024*.

Initialize the swap file
```
sudo dphys-swapfile setup
```
Start swap
```
sudo dphys-swapfile swapon
```
## needed SW installed with apt-get

```
sudo apt-get install screen git
```

## ToDo: add external USB and mount it
https://www.raspberrypi-spy.co.uk/2014/05/how-to-mount-a-usb-flash-disk-on-the-raspberry-pi/

