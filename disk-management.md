## Resize LVM volume
Default LVM main partition size appears to be 4GB on Ubuntu 18.04 Server install

Per [this answer on SO](https://askubuntu.com/a/1117523)

```sh
# We need to resize the logical volume to use all the available space of the volume group
$ lvm
lvm> lvextend -l 100%FREE /dev/ubuntu-vg/ubuntu-lv
lvm> exit

# And then, we need to resize the file system to use the new available space in the logical volume
$ resize2fs /dev/ubuntu-vg/ubuntu-lv
resize2fs 1.44.1 (24-Mar-2018)
Filesystem at /dev/ubuntu-vg/ubuntu-lv is mounted on /; on-line resizing required
old_desc_blocks = 1, new_desc_blocks = 58
The filesystem on /dev/ubuntu-vg/ubuntu-lv is now 120784896 (4k) blocks long.

# Finally, you can check that you now have available space:
$ df -h
Filesystem                         Size  Used Avail Use% Mounted on
udev                               3.9G     0  3.9G   0% /dev
tmpfs                              786M  1.2M  785M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv  454G  3.8G  432G   1% /
```

If you didn't customize the LVM settings, the names for the volume group and logical volume should be the same as mine (`ubuntu-vg` and `ubuntu-lv` respectively).

If your partition is completely full, you could get a `no space left` error when trying to resize the logical volume like:

```sh
lvm> lvextend -l 100%FREE /dev/ubuntu-vg/ubuntu-lv
  /etc/lvm/archive/.lvm_computer: write error failed: No space left on device
```

The easier way to fix this is by removing `apt` cache (it will get regenerated next time you do `apt update`), which should give you more than enough space to complete the operation:

```sh
$ rm -rf /var/cache/apt/*
```

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

## Mounting an LVM volume on an external drive when LVM group name is a duplicate
As in a cloned disk backup... system won't mount the volume because the volume group is a duplicate of the one currently in use, in this case `ubuntu-vg`

[Re: Mounting Ubuntu LVM partition to recover data](https://ubuntuforums.org/showthread.php?t=2290548&p=13338030#post13338030)

> `sudo vgrename /dev/ubuntu-vg /dev/whatever`
    
or

>`sudo vgrename {UUID} /dev/whatever`
    
