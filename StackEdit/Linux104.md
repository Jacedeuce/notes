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
	* The following files are read when "files" source is specified for
       respective databases:

         **aliases** _/etc/aliases_
         **ethers** _/etc/ethers_
         **group** _/etc/group_
         !!!! **hosts** _/etc/hosts_
         **initgroups** _/etc/group_
         **netgroup** _/etc/netgroup_
         **networks** _/etc/networks_
         **passwd** _/etc/passwd_
         **protocols** _/etc/protocols_
         **publickey** _/etc/publickey_
         **rpc** _/etc/rpc_
         **services** _/etc/services_
         **shadow** _/etc/shadow_

### IPv6 interface identifier
* 64 bits 
![Image result for ipv6 interface id](https://docs.oracle.com/cd/E23823_01/html/816-4554/figures/basic-IPv6-address.png)
### TCP Wrapper Encryption
* `tcpd` checks `hosts.allow` and `hosts.deny` for access control to internet services (ssh, telnet, ftp, etc...)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQzMDIzMjU2OCwtMTAyNzM5MDAyNCw2MT
AxODU5MDMsODYwMTg4MTIzLC02MTE3MzM3MTMsMjEyODQyMDU0
NSwtMjE0ODA3MDI2LC0xMTkwNTgwOTc0LC0xNzMwNjE2MzgyLD
c0NzQxOTk3NSwtMjAzOTMxOTAxOCwtMjA2MjIxOTU5MCwtMTUw
Mjc3MDE2NCwtOTA0MTYyODc0LDYwMDQxODQ5NywzODY1MTExOD
ddfQ==
-->