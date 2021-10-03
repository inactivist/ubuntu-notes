## Control `/tmp` cleanup at boot
Edit `/etc/default/rcS` and set `TMPTIME=30` to retain files modified within last 30 days.  Adjust value accordingly.

Source: [Stop Ubuntu / Debian Linux From Deleting /tmp Files on Boot](https://www.cyberciti.biz/faq/debian-ubuntu-removes-files-at-boot-time/)

## Enable/Disable tracker service (search indexer) for current user, 

```bash

# Set ACTION=unmask to enable
export ACTION=mask

systemctl --user $ACTION tracker-store.service tracker-miner-fs.service tracker-miner-rss.service tracker-extract.service tracker-miner-apps.service tracker-writeback.service
```
