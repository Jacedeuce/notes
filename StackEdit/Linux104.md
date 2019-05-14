## Shell Scripting

### IF statement syntax

* if COMMANDS; then COMMANDS; [ elif COMMANDS; then COMMANDS; ]... [ else COMMANDS; ] fi

### function

* creates functions

### $() 

* execute command and replace with value

### Test

* `-e` test if file exists
* `-f` test if file exists and is a regular file
* `=` String comparison
* `-eq` Integer comparison

### iconv
*Convert encoding of given files from one encoding to another*
* iconv **-f** _encoding_ **-t** _encoding inputfile_

### Cron
* fields: minute, hour, day of month, month, day of week, command
`*	*	*	*	*	command`
* **/etc/crontab**

### Batch command

##### at

* executes commands **in parallel** at a specified time. 

##### batch

* **sequentially** executes commands when system load levels permit; in other words, 
when the load average drops below 0.8, or the value specified in 
the invocation of atd. 

##### permitted by the (1) /etc/at.allow and (2) /etc/at.deny



### Managing Shell Variables

##### set

* set - Set or unset values of shell options and positional parameters.

##### export

* export - Set export attribute for shell variables.


## Logging

### syslog.conf
*	redirect to console: ```mail.=info (".") 	/dev/tty12```
### journald
* /etc/system/journald.conf

## User Settings

### BASHRC vs PROFILE

| Global | User | Use |
|---------|-----|------|
| /etc/bashrc | ~/.bashrc | command aliases and functions |
| /etc/profile | ~/.bash_profile | set environment variables |

### /etc/passwd
* `x` marks encrypted password stored in /etc/shadow
### /etc/shadow
* file stores encrypted passwords
* only root has r or w access

### usermod
* `-g` primary group
* `-G` secondary group

### chsh
*change your login shell*
* `-s` specify login shell (/bin/false will disble login)

### Setting the clock
* `hwclock` *-w*, (*--systohc*) or *-s*, *--hctosys*

### timezone
* set by **/etc/localtime** */etc/timezone*, linked to **/usr/share/zoneinfo**
* converted using standard libraries in /usr/share

## X

### Display Manager
* Is started by the init system
* Start and set up the Desktop Environment
* Handle user login after system startup

### XDM
*X Display Manager*
* Set wallpaper: ``/etc/X11/xdm/Xsetup``

### GDM
* /etc/gdm/custom.conf or `gdmsetup`- set greeting

### X Server
* Instances are identified by a display name like `1.`
* access is managed by `xhost`:
	* server access control program for X
* ?`xcolordepth` command displays color depth for X Server
	> xwininfo -root | grep Depth
* `~/.Xdefaults` sets user configuration changes (window size, location, color)

### xorg.conf
* Sections are bracketed by **SectionName** and **EndSection**
```
SectionName
# text
# text
option=text
# text
EndSection
```
* **Files** section manages **fonts**

## Printing

## User Accessibility

### GOK
* **G**NOME **O**n-screen **K**eyboard

## Networking

### nsswitch.conf
* configures where the C library looks for system information (host names, user passwords).

### IPv6 interface identifier
* 64 bits


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI1MTE0MzQ5NSw2MTAxODU5MDMsODYwMT
g4MTIzLC02MTE3MzM3MTMsMjEyODQyMDU0NSwtMjE0ODA3MDI2
LC0xMTkwNTgwOTc0LC0xNzMwNjE2MzgyLDc0NzQxOTk3NSwtMj
AzOTMxOTAxOCwtMjA2MjIxOTU5MCwtMTUwMjc3MDE2NCwtOTA0
MTYyODc0LDYwMDQxODQ5NywzODY1MTExODddfQ==
-->