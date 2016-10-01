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
