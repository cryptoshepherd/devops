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


Reboot the device
```

```sh
You should now be able to see the Wifi connected to the SSID specified 
```


## Meta

Simone Arena – @the_lello – lellothegreat@protonmail.ch
