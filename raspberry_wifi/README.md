# RaspberryPi Wifi
> Procedure to configure an External Wifi Dongle

![](header.png)

## Disable the internal Wifi

```sh
sudo nano /boot/config.txt

---
dtoverlay=pi3-disable-wifi
---

sudo nano /etc/modprobe.d/raspi-blacklist.conf

---
blacklist brcmfmac
blacklist brcmutil
---

Reboot the device

```

```sh

If you are ok like to have an IP address assigned via DCHP, you just need to edit the following

sudo nano /etc/wpa_supplicant/wpa_supplicant.conf

---
country=DE
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
        ssid="YOUR_SSID"
        psk="YOUR_WiFi_PASSWD"
        key_mgmt=WPA-PSK
 }
---

sudo nano /etc/network/interfaces

---
auto lo

iface lo inet loopback
iface eth0 inet dhcp

allow-hotplug wlan0
auto wlan0


iface wlan0 inet dhcp
wpa-conf /etc/wpa_supplicant/wpa_supplicant.conf
---


Reboot the device
```

```sh
You should now be able to see the Wifi connected to the SSID specified 
```


## Meta

Simone Arena – @the_lello – lellothegreat@protonmail.ch
