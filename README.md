# Build LTE Modem Kernel Driver
### Install Necessary Libraries
```sudo apt-get install gcc make libncurses5-dev openssl libssl-dev```
```sudo apt-get install build-essential``` 
```sudo apt-get install pkg-config```
```sudo apt-get install libc6-dev```
```sudo apt-get install bison```
```sudo apt-get install flex```
```sudo apt-get install libelf-dev```
### Build Kernel locally
``` sudo apt-get install linux-image-`uname -r` ```
```cd ~/usr/src/linux-4.15.18```
```sudo cp /boot/config-4.15.0-20-generic .config```
```sudo make menuconfig```

>[\*] Device Drivers → 
>>[\*] USB Support → 
>>>[\*] USB Serial Converter support → 
>>>>[\*] USB driver for GSM and CDMA modems 

>[\*] Device Drivers → 
>>[\*] Network device support → 
>>>[\*] PPP (point-to-point protocol) support 

 			
>[\*] Device Drivers → 
>>-\*- Network device support → 
>>>USB Network Adapters → 
>>>>{\*} Multi-purpose USB Networking Framework 
>>>>><\*> QMI WWAN driver for Qualcomm MSM based 3G and LTE modems

```sudo make```
```sudo make INSTALL_MOD_STRIP=1 modules_install```

```sudo make install```
```sudo mkinitramfs -o /boot/initrd.img-4.15.18```
```sudo update-initramfs -c -k 4.15.18```
```sudo update-grub2```
### Build Kernel Deb Package
```cd ~/usr/src/linux-4.15.18```
```sudo cp /boot/config-4.15.0-20-generic .config```
```sudo make menuconfig```
>[\*] Device Drivers → 
>>[\*] USB Support → 
>>>[\*] USB Serial Converter support → 
>>>>[\*] USB driver for GSM and CDMA modems 

>[\*] Device Drivers → 
>>[\*] Network device support → 
>>>[\*] PPP (point-to-point protocol) support 

 			
>[\*] Device Drivers → 
>>-\*- Network device support → 
>>>USB Network Adapters → 
>>>>{\*} Multi-purpose USB Networking Framework 
>>>>><\*> QMI WWAN driver for Qualcomm MSM based 3G and LTE modems

```sudo make oldconfig```

```set CONFIG_SYSTEM_TRUSTED_KEYS = ""```
```set CONFIG_DEBUG_INFO=n```

```make -j3 deb-pkg```

```sudo dpkg -i linux-image-4.15.18_4.15.18-1_amd64.deb```
```sudo dpkg -i linux-headers-4.15.18_4.15.18-1_amd64.deb```
```sudo update-grub2```
```sudo reboot```
