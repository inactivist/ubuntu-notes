## Determine physical sector size
```bash
$ sudo hdparm -I /dev/sda | grep -i physical
Physical Sector size:                  4096 bytes
```
[ref](http://superuser.com/a/426015)

## Disk cloning

```bash
# dd if=/dev/sdX conv=sync,noerror bs=64K | gzip -c  > /path/to/backup.img.gz
```
From: [Disk cloning guide](https://wiki.archlinux.org/index.php/disk_cloning)

## Mounting a raw disk image
```bash
losetup /dev/loop1 /home/backup-file
mount /dev/loop1 /mnt/backup 
```
[ref](http://superuser.com/a/488888)

## Mounting an LVM volumen on an external drive when LVM group name is a duplicate
As in a cloned disk backup... system won't mount the volume because the volume group is a duplicate of the one currently in use, in this case `ubuntu-vg`

[Re: Mounting Ubuntu LVM partition to recover data](https://ubuntuforums.org/showthread.php?t=2290548&p=13338030#post13338030)

> `sudo vgrename /dev/ubuntu-vg /dev/whatever`
    
or

>`sudo vgrename {UUID} /dev/whatever`
    
