### VirtualBox and secure boot module signing under Ubuntu 18.04
(This information archived from [VirtualBox + Secure Boot + Ubuntu = fail](https://stegard.net/2016/10/virtualbox-secure-boot-ubuntu-fail/))

Install the virtualbox package. If the installation detects that Secure Boot is enabled, you will be presented with the issue at hand and given the option to disable Secure Boot. Choose “No”.
Create a personal public/private RSA key pair which will be used to sign kernel modules. I chose to use the root account and the directory /root/module-signing/ to store all things related to signing kernel modules.

```bash
$ sudo -i
# mkdir /root/module-signing
# cd /root/module-signing
# openssl req -new -x509 -newkey rsa:2048 -keyout MOK.priv -outform DER -out MOK.der -nodes -days 36500 -subj "/CN=YOUR_NAME/"
[...]
# chmod 600 MOK.priv
```
Use the MOK (“Machine Owner Key”) utility to import the public key so that it can be trusted by the system. This is a two step process where the key is first imported, and then later must be enrolled when the machine is booted the next time. A simple password is good enough, as it is only for temporary use.
```bash
# mokutil --import /root/module-signing/MOK.der
input password:
input password again:
```
Reboot the machine. When the bootloader starts, the MOK manager EFI utility should automatically start. It will ask for parts of the password supplied in step 3. Choose to “Enroll MOK”, then you should see the key imported in step 3. Complete the enrollment steps, then continue with the boot. The Linux kernel will log the keys that are loaded, and you should be able to see your own key with the command: dmesg|grep 'EFI: Loaded cert'
Using a signing utility shippped with the kernel build files, sign all the VirtualBox modules using the private MOK key generated in step 2. I put this in a small script /root/module-signing/sign-vbox-modules, so it can be easily run when new kernels are installed as part of regular updates:

```bash
#!/bin/bash

for modfile in $(dirname $(modinfo -n vboxdrv))/*.ko; do
  echo "Signing $modfile"
  /usr/src/linux-headers-$(uname -r)/scripts/sign-file sha256 \
                                /root/module-signing/MOK.priv \
                                /root/module-signing/MOK.der "$modfile"
done
```

```
# chmod 700 /root/module-signing/sign-vbox-modules
```

Run the script from step 5 as root. You will need to run the signing script every time a new kernel update is installed, since this will cause a rebuild of the third party VirtualBox modules. Use the script only after the new kernel has been booted, since it relies on modinfo -n and uname -r to tell which kernel version to sign for.
Load vboxdrv module and fire up VirtualBox:
```
# modprobe vboxdrv
```

The procedure can also be used to sign other third party kernel modules, like the nvidia graphics drivers, if so is required. (I have not tested that myself.)

