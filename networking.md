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
- [Auto-switch between ethernet and wifi](https://matoski.com/article/wifi-ethernet-autoswitch/) (via [this SO answer](https://unix.stackexchange.com/a/509072/117411))
