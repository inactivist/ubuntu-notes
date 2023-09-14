## FlatPak filesystem access (sandbox)

Help!  FlatPak installed Gimp won't open files in home directory!


```bash
sudo flatpak override org.gimp.GIMP --filesystem=${full-path}
```

[source](https://askubuntu.com/questions/1086529/how-to-give-a-flatpak-app-access-to-a-directory/1094903#1094903)


## Control `/tmp` cleanup at boot
Edit `/etc/default/rcS` and set `TMPTIME=30` to retain files modified within last 30 days.  Adjust value accordingly.

Source: [Stop Ubuntu / Debian Linux From Deleting /tmp Files on Boot](https://www.cyberciti.biz/faq/debian-ubuntu-removes-files-at-boot-time/)

## Enable/Disable tracker service (search indexer) for current user, 

```bash

# Set ACTION=unmask to enable
export ACTION=mask

# the long way
systemctl --user $ACTION tracker-store.service tracker-miner-fs.service tracker-miner-rss.service tracker-extract.service tracker-miner-apps.service tracker-writeback.service

# shorter
systemctl --user $ACTION tracker-{miner-apps,miner-fs,store}

```

### More info:

- [linuxquestions](https://www.linuxquestions.org/questions/ubuntu-63/how-to-disable-tracker-globally-in-ubuntu-20-04-a-4175678847/#post6146134)
- [Tracker Wiki](https://wiki.ubuntu.com/Tracker)
