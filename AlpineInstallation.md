# Download Alpine Linux

- Download [Alpine](https://www.alpinelinux.org/downloads/) Standard / Extended

# Alpine Installation
Boot from Alpine iso

login
```
localhost login: root
```
start alpine installer
```
setup-alpine
```
```
Keymap: us
```
```
keyboard layout: us
```
```
system hostname: localhost or alpine-linux
```
```
interface: eth0
```
```
ip address for interface: dhcp
```
```
Do you want to do any manual network configuration? [y/n]: n
```
Root Password: 
```
New password: 1234
```
```
Retype password: 1234
```
Timezone:
```
Which time zone are you in?: <your-timezone>
```
```
What sub-timezone are you in?: <your-sub-timezone>
```
```
Proxy: none
```
```
Network Time Protocol: chrony
```
```
APK Mirrror: c
```
```
Enter mirror URL: dl-cdn.alpinelinux.org or press Enter Key
```
```
loginname: <your-username>
```
```
Full name for user: <your-fullname>
```
```
New password: 1234
```
```
Retype password: 1234
```
```
Enter ssh key or URL for user: none
```
```
Which ssh server: openssh
```
```
Which disk would you like to use: sda
```
```
How would like to use it: sys
```
```
Erase the above disk and continue? (y/n): y 
```
```
su -
```
```
apk update
```
```
apk add sudo
```
```
echo "<your-username> ALL=(ALL:ALL) ALL" >> /etc/sudoers
```
```
adduser <your-username> wheel
```
```
exit
```
Remove bootable iso
```
sudo reboot
```
```
alpine-linux login: <your-username>
```
```
Password: 1234
```
```
cat /etc/os-release
```

Alpine GUI Installation
```
sudo setup-desktop or su -c "setup-desktop"
```
```
Which desktop environment?: gnome
```
```
sudo reboot or su -c "reboot"
```
```
from gnome desktop env login using <your-password:1234>
```
Open Gnome Console (Terminal)
```
sudo -s
```
```
su -c "apk update && apk add sudo"
```
```
su -c 'echo "<your-username> ALL=(ALL:ALL) ALL" >> /etc/sudoers'
```
```
su -c "adduser <your-username> wheel"
```
```
su -c "reboot"
```
```
from gnome desktop env login using <your-password:1234>
```
Open Gnome Console (Terminal)
```
sudo -s
```
```
exit
```
```
echo $SHELL
```
```
sudo apk add bash
```
```
chsh -s $(which bash) or chsh -s /bin/bash
```
```
exit
```
Open Gnome Console (Terminal)
```
echo $SHELL
```
---