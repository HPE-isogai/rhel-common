- Link
https://pfs.nifcloud.com/guide/cp/login/mount_linux.htm

- Procedure
```
[newgen@rhel8-iso ~]$ sudo -i
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# lsblk
NAME                     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                        8:0    0   32G  0 disk
├─sda1                     8:1    0  600M  0 part /boot/efi
├─sda2                     8:2    0    1G  0 part /boot
└─sda3                     8:3    0 30.4G  0 part
  ├─rhel_rhel8--iso-root 253:0    0 27.2G  0 lvm  /
  └─rhel_rhel8--iso-swap 253:1    0  3.2G  0 lvm  [SWAP]
sdb                        8:16   0  150G  0 disk
sr0                       11:0    1 1024M  0 rom
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# fdisk
fdisk: bad usage
Try 'fdisk --help' for more information.
[root@rhel8-iso ~]# fdisk -l
Disk /dev/sdb: 150 GiB, 161061273600 bytes, 314572800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sda: 32 GiB, 34359738368 bytes, 67108864 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 63B8D4CE-7590-4786-8BBA-086856F4DCAE

Device       Start      End  Sectors  Size Type
/dev/sda1     2048  1230847  1228800  600M EFI System
/dev/sda2  1230848  3327999  2097152    1G Linux filesystem
/dev/sda3  3328000 67106815 63778816 30.4G Linux LVM




Disk /dev/mapper/rhel_rhel8--iso-root: 27.2 GiB, 29213327360 bytes, 57057280 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/rhel_rhel8--iso-swap: 3.2 GiB, 3439329280 bytes, 6717440 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.32.1).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table.
Created a new DOS disklabel with disk identifier 0xd90dddd9.

Command (m for help): n
Partition type
   p   primary (0 primary, 0 extended, 4 free)
   e   extended (container for logical partitions)
Select (default p): p
Partition number (1-4, default 1): 1
First sector (2048-314572799, default 2048):
Last sector, +sectors or +size{K,M,G,T,P} (2048-314572799, default 314572799):

Created a new partition 1 of type 'Linux' and of size 150 GiB.

Command (m for help):


Command (m for help): p

Disk /dev/sdb: 150 GiB, 161061273600 bytes, 314572800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xd90dddd9

Device     Boot Start       End   Sectors  Size Id Type
/dev/sdb1        2048 314572799 314570752  150G 83 Linux

Command (m for help): w
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.

[root@rhel8-iso ~]#
[root@rhel8-iso ~]# partprobe
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# fdisk -l
Disk /dev/sdb: 150 GiB, 161061273600 bytes, 314572800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xd90dddd9

Device     Boot Start       End   Sectors  Size Id Type
/dev/sdb1        2048 314572799 314570752  150G 83 Linux


Disk /dev/sda: 32 GiB, 34359738368 bytes, 67108864 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: 63B8D4CE-7590-4786-8BBA-086856F4DCAE

Device       Start      End  Sectors  Size Type
/dev/sda1     2048  1230847  1228800  600M EFI System
/dev/sda2  1230848  3327999  2097152    1G Linux filesystem
/dev/sda3  3328000 67106815 63778816 30.4G Linux LVM




Disk /dev/mapper/rhel_rhel8--iso-root: 27.2 GiB, 29213327360 bytes, 57057280 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/rhel_rhel8--iso-swap: 3.2 GiB, 3439329280 bytes, 6717440 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# mkfs -t ext4 /dev/sdb1
mke2fs 1.45.6 (20-Mar-2020)
Discarding device blocks: done
Creating filesystem with 39321344 4k blocks and 9830400 inodes
Filesystem UUID: 969117d7-7139-4305-bb23-a5d72e92acb8
Superblock backups stored on blocks:
        32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
        4096000, 7962624, 11239424, 20480000, 23887872

Allocating group tables: done
Writing inode tables: done
Creating journal (262144 blocks): done
Writing superblocks and filesystem accounting information: done

[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# mkdir /nfs
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# blkid
/dev/sdb1: UUID="969117d7-7139-4305-bb23-a5d72e92acb8" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="d90dddd9-01"
/dev/sda1: UUID="6DDF-2E4C" BLOCK_SIZE="512" TYPE="vfat" PARTLABEL="EFI System Partition" PARTUUID="a81ab34f-a9f8-4cba-9227-59c09b1017e9"
/dev/sda2: UUID="027472a3-3e3f-42f1-a16c-40cc9432bef7" BLOCK_SIZE="512" TYPE="xfs" PARTUUID="c1262d2b-774d-498d-91f9-421f94221f6e"
/dev/sda3: UUID="2I0wER-7cMe-Lv3S-bsrN-vjQl-wrBm-aJCpET" TYPE="LVM2_member" PARTUUID="038a0010-ae5e-4009-9bfe-0433b028b28f"
/dev/mapper/rhel_rhel8--iso-root: UUID="fe793226-db05-4052-8508-0c63cbe6e161" BLOCK_SIZE="512" TYPE="xfs"
/dev/mapper/rhel_rhel8--iso-swap: UUID="e4e01c23-c2ef-4a5f-bdc0-62562a567050" TYPE="swap"
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# vim /etc/fstab
[root@rhel8-iso ~]#
[root@rhel8-iso ~]#
[root@rhel8-iso ~]# mount /dev/sdb1 /nfs
[root@rhel8-iso ~]# df -h
Filesystem                        Size  Used Avail Use% Mounted on
devtmpfs                          2.8G     0  2.8G   0% /dev
tmpfs                             2.9G     0  2.9G   0% /dev/shm
tmpfs                             2.9G  9.6M  2.8G   1% /run
tmpfs                             2.9G     0  2.9G   0% /sys/fs/cgroup
/dev/mapper/rhel_rhel8--iso-root   28G  6.1G   22G  23% /
/dev/sda2                        1014M  235M  780M  24% /boot
/dev/sda1                         599M  6.9M  592M   2% /boot/efi
tmpfs                             576M  1.2M  574M   1% /run/user/42
tmpfs                             576M  4.6M  571M   1% /run/user/1000
/dev/sdb1                         147G   61M  140G   1% /nfs
```
