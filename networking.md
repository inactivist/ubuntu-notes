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

