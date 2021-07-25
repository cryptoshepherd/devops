# Product Name
> KVM Installation Manjaro

KVM and Libvirt installation on Manjaro

![](header.png)

## Packages Installation

```sh
sudo pacman -S qemu virt-manager virt-viewer dnsmasq vde2 bridge-utils openbsd-netcat
```

```sh
sudo pacman -S ebtables iptables
```

## Optional 

```sh
sudo vim /etc/pacman.conf

# Should have below lines
[archlinuxfr]
SigLevel = Never
Server = http://repo.archlinux.fr/$arch

sudo pacman -Syy

sudo pacman -S yaourt
yaourt -S --noconfirm --needed libguestfs
```

## Start Services

```sh
sudo systemctl enable libvirtd.service
sudo systemctl start libvirtd.service

sudo systemctl status libvirtd.service
```

## Enable normal user account

```sh
sudo pacman -S vim
sudo vim /etc/libvirt/libvirtd.conf

unix_sock_group = "libvirt"
unix_sock_rw_perms = "0770"

sudo usermod -a -G libvirt $(whoami)
newgrp libvirt

sudo systemctl restart libvirtd.service
```

## Install vagrant libvirt pluging

```sh
vagrant plugin install vagrant-libvirt
```

## Confiure a br0 (Bridge interface to be used in conjunction with Vagrant 

```sh
nmcli connection show

---
NAME                UUID                                  TYPE      DEVICE
Wired connection 1  f1a2ac88-cc06-363d-81d3-3a9eb279eec1  ethernet  eno1   
docker0             c0300fb0-b7b5-4e79-895e-3dc0a1d66f9b  bridge    docker0 
virbr0              cf557cc1-9a39-432e-8f63-0e9438916e64  bridge    virbr0  
virbr1              25b85213-80bc-41ff-8056-9ebe22195c8f  bridge    virbr1  
virbr2              221ecd99-0832-40b7-ae48-714c52a7b4d2  bridge    virbr2  
---

sudo nmcli con add ifname br0 type bridge con-name br0
sudo nmcli con add type bridge-slave ifname eno1 master br0
sudo nmcli con modify br0 bridge.stp no
sudo nmcli con modify br0 bridge.forward-delay 0
sudo nmcli con down "Wired connection 1" && sudo nmcli con up br0
sudo nmcli con show


---
NAME                UUID                                  TYPE      DEVICE  
br0                 ae124643-9956-4a08-9186-7e5dcd72ec03  bridge    br0     
docker0             c0300fb0-b7b5-4e79-895e-3dc0a1d66f9b  bridge    docker0 
virbr0              cf557cc1-9a39-432e-8f63-0e9438916e64  bridge    virbr0  
virbr1              25b85213-80bc-41ff-8056-9ebe22195c8f  bridge    virbr1  
virbr2              221ecd99-0832-40b7-ae48-714c52a7b4d2  bridge    virbr2  
bridge-slave-eno1   1dd33478-5bcb-47fc-aebf-48f1e58d6f6b  ethernet  eno1    
vnet0               80e609ef-1b79-4388-8651-193aef3ca93b  tun       vnet0   
vnet1               a5724a43-f44f-49ae-9912-40542b5d2670  tun       vnet1   
vnet2               7f253ea0-1159-4357-a559-ce2af7b4ad6d  tun       vnet2   
vnet3               c87ad489-21c7-4d09-acf6-511bbd96e461  tun       vnet3   
vnet4               ffa593e5-3248-426d-8d86-cedfed19ca83  tun       vnet4   
vnet5               f9fabf50-762d-43a6-ba86-73ad5da72d4f  tun       vnet5   
vnet6               2ecc72b6-e056-4d69-8382-272ecf5542ee  tun       vnet6   
vnet7               0be6b879-1e3a-400e-b623-7e4da9f75f4c  tun       vnet7   
Wired connection 1  f1a2ac88-cc06-363d-81d3-3a9eb279eec1  ethernet  --
---
```

## Optional, set static ip/net

```sh
sudo nmcli con mod br0 ipv4.addresses 192.168.0.10/24

sudo nmcli con mod br0 ipv4.gateway 192.168.0.1

sudo nmcli con mod br0 ipv4.dns "8.8.8.8","192.168.0.1"

sudo nmcli con mod br0 ipv4.method manual
```


## Meta

Your Name – [@YourTwitter](https://twitter.com/the_lello) – lellothegreat@protonmail.ch

Distributed under the GNU license. See ``LICENSE`` for more information.

