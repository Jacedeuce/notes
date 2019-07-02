## Fedora Set Up log
```console
dnf upgrade --refresh
```
### Settings
#### Set key binding for gnome-terminal
settings>devices>keyboard set:
* ctl+alt+t for gnome-terminal

#### under settings>devices>monitor:
* set orientation

#### under settings>devices>mouse:
* tap to click on touchpad

### Install KeePass:
```console
dnf install keepass
```

### [Install vscode](https://code.visualstudio.com/docs/setup/linux)
#### [Install Extensions](https://github.com/Jacedeuce/notes/blob/master/StackEdit/Coding%20Dojo/20190520_First%20Day.md)


### Install Node.js
[instructions](https://tecadmin.net/install-latest-nodejs-on-fedora/)

### Install Chromium
```console
sudo dnf install chromium
```

### Install Pandora
[Flatpak](https://nuvola.tiliado.eu/app/pandora/fedora/fc28/)

https://docs.fedoraproject.org/en-US/quick-docs/setup_rpmfusion/
https://rpmfusion.org/Configuration
This One! --> https://forums.fedoraforum.org/showthread.php?317721-fedora-28-and-firefox-video(h264-youtube-gstreamer1)

no headphone sound: 
* ```/usr/bin/amixer -c0 set Headphone unmute 100% ```Install Flash

Install H.264 codec

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwNDIxMjEwMzcsMTk1Mjc2Mjk3NSwtMT
YzOTAyOTk2Myw0NTUwMjA1NDYsMTc4ODQ4MzM1NCw0ODU0MjI4
OTMsLTExNzM3MTQ3MDJdfQ==
-->