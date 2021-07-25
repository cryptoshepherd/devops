# Internal disk partition and mount
> Procedure to format and mount a new internal disk at boot

![](header.png)

## Disk Partitioning (if > 2TB use parted instead)

```sh
sudo mkdir /mediatwo (create the mount point folder you wish)
sudo fdisk -l

---
Disk /dev/sda: 256.17 GiB, 275064201216 bytes, 537234768 sectors
Disk model: Crucial_CT275MX3
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x9a2baf4b
---

sudo fdisk /dev/sda

Command (m for help): n <--
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)

Select (default p): p <--
Partition number (1-4, default 1): 1 <-- ENTER
First sector (2048-537234767, default 2048): <-- ENTER
Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-537234767, default 537234767): <-- ENTER (will takes all the disk) 

Created a new partition 1 of type 'Linux' and of size 256.2 GiB.
Partition #1 contains a ext4 signature.

Command (m for help): w <--
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

```

```sh

sudo fdisk -l

---
Disk /dev/sda: 256.17 GiB, 275064201216 bytes, 537234768 sectors
Disk model: Crucial_CT275MX3
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x9a2baf4b

Device     Boot Start       End   Sectors   Size Id Type
/dev/sda1        2048 537234767 537232720 256.2G 83 Linux     ---> !
---


sudo mkfs -t ext4 /dev/sda1
```

```sh
lsblk -no UUID /dev/sda1
lsblk -no FSTYPE /dev/sda1

sudo vim /etc/fstab

---
UUID=356058ff-5657-4bd9-9f42-d04d4c018e42 /datatwo ext4 defaults,noatime 0 2
---
```

Reboot your system

NOTE: if the mount point created is outside your home folders:

```sh
sudo chmod ugo+rwx /mediatwo
```


## Meta

Simone Arena – @the_lello – lellothegreat@protonmail.ch
