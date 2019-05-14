## Shell Scripting

### Test

* -e test if file exists
* -f test if file exists and is a regular file
* = String comparison
* -eq Integer comparison

### function

* creates functions

### $() 

* execute command and replace with value

### Batch command

##### at

* executes commands at a specified time. 

##### batch

* executes commands when system load levels permit; in other words, 
when the load average drops below 0.8, or the value specified in 
the invocation of atd. 

##### permitted by the (1) /etc/at.allow and (2) /etc/at.deny

### Managing Shell Variables

##### set

* set - Set or unset values of shell options and positional parameters.

##### export

* export - Set export attribute for shell variables.

### IF statement syntax

* if COMMANDS; then COMMANDS; [ elif COMMANDS; then COMMANDS; ]... [ else COMMANDS; ] fi


## User Settings

### BASHRC vs PROFILE

| Global | User | Use |
|---------|-----|------|
| /etc/bashrc | ~/.bashrc | command aliases and functions |
| /etc/profile | ~/.bash_profile | set environment variables |


## X

### Display Manager
* Is started by the init system
* Start and set up the Desktop Environment
* Handle user login

### XDM
*X Display Manager*
* Set wallpaper: ``/etc/X11/xdm/Xsetup``

### X Server
* Instances are identified by a display name like `1.`

### xorg.conf Sections
* Sections are bracketed by **SectionName** and **EndSection**
```
SectionName
# text
# text
option=text
# text
EndSection
``` 

### xcolordepth
* displays color depth of X Server


## User Accessibility

### GOK
* **G**NOME **O**n-screen **K**eyboard


<!--stackedit_data:
eyJoaXN0b3J5IjpbNjU0ODQyMTUyLC05MDQxNjI4NzQsNjAwND
E4NDk3LDM4NjUxMTE4N119
-->