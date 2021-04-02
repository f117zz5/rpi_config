# Installing the rtl-sdr drivers

Original article [here](https://www.az-delivery.de/blogs/azdelivery-blog-fur-arduino-und-raspberry-pi/raspberry-headless-setup-rtl-sdr). 

First install the needed SW to build the drivers:
```
sudo apt-get install git git-core cmake libusb-1.0-0-dev build-essential
```

Then clone the repository:
```
git clone git://git.osmocom.org/rtl-sdr.git
```
As I had problems with the permissions after that, I had to:
```
git checkout f2a9a81
```
RPi chrashed several times, I am trying with **f68bb2f** now.

Then:
```
cd rtl-sdr/
mkdir build
cd build/
cmake ../ -DINSTALL_UDEV_RULES=ON
sudo make
sudo make install
```
then continue with:
```
sudo ldconfig
cd ..
sudo cp ./rtl-sdr.rules /etc/udev/rules.d/
```

Disable the original driver:
```
cd /etc/modprobe.d/
nano no-rtl.conf
blacklist dvb_usb_rtl28xxu
blacklist rtl_2830
blacklist rtl_2832
```
reboot...
```
sudo reboot
```



# multimon-ng install

Clone the repository here: https://github.com/EliasOenal/multimon-ng

Then:
```
mkdir build
cd build
qmake ../multimon-ng.pro
make
sudo make install
```
On Raspberry Pi with Raspbian GNU/Linux 10 (buster) the installation compleined about missing PulseAudio libs, but it was OK. 



# dump1090

testing docker was very time consuming and frustrating. Check later the instructions here:
https://weberblog.net/ads-b-am-raspberry-pi-dump1090-mutability/
https://blog.alexellis.io/track-flights-with-rpi/
