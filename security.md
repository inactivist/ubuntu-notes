## Firewalls
- Improve firewall integration with Network Manager (switch firewall profiles based on network connection)
  - Install `firewalld`:  `sudo apt-get install firewall-applet` [ref](http://linuxbsdos.com/2013/06/26/how-to-replace-ufw-with-firewalld-in-linux-mint-15/)

## Groups
### Add a user to an existing group, reload groups

https://superuser.com/a/853897


1. Getting a shell with the new group without logging out and in again

If you're only adding one group, I used the following:

    exec sg <new group name> newgrp `id -gn`

This is a variation on Legooolas's two-layer newgrp trick, but it is in one line and doesn't require you to manually enter your primary group.

`sg` is newgrp but accepting a command to execute with the new group ID. The `exec` means that the new shell replaces the existing shell, so you don't need to "logout" twice.

Unlike using su, you don't need to type in your password. It also doesn't refresh your environment (other than adding the group), so you retain your current working directory etc.

