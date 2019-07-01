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

no headphone sound: 
* ```/usr/bin/amixer -c0 set Headphone unmute 100% ```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzkwMjk5NjMsNDU1MDIwNTQ2LDE3OD
g0ODMzNTQsNDg1NDIyODkzLC0xMTczNzE0NzAyXX0=
-->