# KVM on Ubuntu
> KVM Installation Ubuntu

KVM and Libvirt installation on Manjaro

![](header.png)

## Packages Installation and Services start

```sh
sudo apt install qemu qemu-kvm libvirt-clients libvirt-daemon-system virtinst bridge-utils
```

```sh
sudo systemctl enable libvirtd

sudo systemctl start libvirtd

systemctl status libvirtd
```


## Bridge 

```sh
sudo vi /etc/sysctl.d/bridge.conf

---
net.bridge.bridge-nf-call-ip6tables=0
net.bridge.bridge-nf-call-iptables=0
net.bridge.bridge-nf-call-arptables=0
---

sudo vi /etc/udev/rules.d/99-bridge.rules

---
ACTION=="add", SUBSYSTEM=="module", KERNEL=="br_netfilter", RUN+="/sbin/sysctl -p /etc/sysctl.d/bridge.conf"
---

sudo reboot

```

## Destroy current network default

```sh
virsh net-destroy default

virsh net-undefine default
```

## Confiure a br0 (Bridge interface to be used by your VMs

```sh
sudo vi /etc/netplan/00-installer-config.yaml

---
# This is the network config written by 'subiquity'
network:
  ethernets:
    enp3s0:
      dhcp4: false
      dhcp6: false
  bridges:
    br0:
      interfaces: [ enp3s0 ]
      addresses: [192.168.178.100/24]
      gateway4: 192.168.178.1
      mtu: 1500
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
      parameters:
        stp: true
        forward-delay: 4
      dhcp4: no
      dhcp6: no
  version: 2  
---

sudo netplan --debug  apply

vi host-bridge.xml

---
<network>
  <name>host-bridge</name>
  <forward mode="bridge"/>
  <bridge name="br0"/>
</network>
---

virsh net-define host-bridge.xml
virsh net-start host-bridge
virsh net-autostart host-bridge
virsh net-list --all

---
Name          State    Autostart   Persistent
------------------------------------------------
 host-bridge   active   yes         yes
---
```

## Install Cockpi


```
sudo apt-get install cockpit cockpit-machines

https://localhost:9090 (or) https://IP-address:9090

```



## Meta

Your Name – [@the_lello](https://twitter.com/the_lello) – lellothegreat@protonmail.ch
