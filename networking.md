## Flushing DNS cache
###  Ubuntu 16.04
```bash
$ sudo /etc/init.d/dns-clean
```
[Reference](http://www.makeuseof.com/tag/flush-dns-cache-ubuntu/)

### Ubuntu 17.04
```bash
$ sudo systemd-resolve --flush-caches
$ sudo systemd-resolve --statistics
```
[Reference](https://askubuntu.com/a/909173)


## Miscellany

### Wired LAN precedence over wireless

- TODO: nmcli set routing metric to prefer wired over wireless
- [How can I make ethernet take precedence over wifi on Ubuntu 18.04?](https://unix.stackexchange.com/questions/494864/how-can-i-make-ethernet-take-precedence-over-wifi-on-ubuntu-18-04)
- [How do I configure a linux machine to ignore wifi when connected via LAN?
](https://superuser.com/questions/630981/how-do-i-configure-a-linux-machine-to-ignore-wifi-when-connected-via-lan)

### Auto Switch between ethernet and wifi based on connection status
- [Auto-switch between ethernet and wifi](https://matoski.com/article/wifi-ethernet-autoswitch/) (via [this SO answer](https://unix.stackexchange.com/a/509072/117411))


Open up your favorite editor and create the file below with the contents.

/etc/NetworkManager/dispatcher.d/70-wifi-wired-exclusive.sh

```
#!/usr/bin/env bash

name_tag="wifi-wired-exclusive"
syslog_tag="$name_tag"
skip_filename="/etc/NetworkManager/.$name_tag.disabled"

if [ -f "$skip_filename" ]; then
  logger -i -t "$syslog_tag $skip_filename present, $name_tag disabled"  
  exit 0
fi

interface="$1"
iface_mode="$2"
iface_type=$(nmcli dev | grep "$interface" | tr -s ' ' | cut -d' ' -f2)
iface_state=$(nmcli dev | grep "$interface" | tr -s ' ' | cut -d' ' -f3)

logger -i -t "$syslog_tag" "Interface: $interface = $iface_state ($iface_type) is $iface_mode"

enable_wifi() {
   logger -i -t "$syslog_tag" "Interface $interface ($iface_type) is down, enabling wifi ..."
   nmcli radio wifi on
}

disable_wifi() {
   logger -i -t "$syslog_tag" "Disabling wifi, ethernet connection detected."
   nmcli radio wifi off
}

if [ "$iface_type" = "ethernet" ] && [ "$iface_mode" = "down" ]; then
  enable_wifi
elif [ "$iface_type" = "ethernet" ] && [ "$iface_mode" = "up"  ] && [ "$iface_state" = "connected" ]; then
  disable_wifi
fi
```
If we want to disable this script, instead of deleting it we can just do

    touch /etc/NetworkManager/.wifi-wired-exclusive.disabled

And this will skip the script everytime it’s invoked.
