# Network Automation with Python

  

## Set Up

  [Join Meeting](https://zoom.us/w/973718255?tk=Sq2CJeufiHroOrJ7uwJO2wS1ZCQureZI7zkCsn_a-Z8.DQEAAAAAOgnC7xZSZGNZZjYzUFR5V0QxNE5hbnhqcmhnAA)

### Instructor

* Sam Griffith

  

### Zoom meeting

```

Or iPhone one-tap

US: +16465588656,,973718255# or +17207072699,,973718255#

Or Telephone:

Dial(for higher quality, dial a number based on your current location):

US: +1 646 558 8656 or +1 720 707 2699

Meeting ID: 973 718 255

International numbers available: [https://zoom.us/u/acjTDDE5QG](https://zoom.us/u/acjTDDE5QG)

```

  

### Virtual Machine

* Console: [https://labs.alta3.com/tmux/napya-401-bchd](https://labs.alta3.com/tmux/napya-401-bchd)

* Static: [https://labs.alta3.com/static/napya-401-bchd/](https://labs.alta3.com/static/napya-401-bchd/)

* GUI: https://labs.alta3.com/?path=view/napya-401-bchd

* examples: [https://labs.alta3.com/static/napya-394-bchd/](https://labs.alta3.com/static/napya-394-bchd/)

  

### TMUX

> Tool to allow multiple windows in command line

  

>  [Cheatsheet]([https://alta3.com/static/posters/tmux.pdf](https://alta3.com/static/posters/tmux.pdf))

>

> ctrl-B opens the tmux prompt

>

> ctrl-B, [ allows scrollup

*  [TMUX Cheatsheet]([https://gist.github.com/andreyvit/2921703](https://gist.github.com/andreyvit/2921703))

### Vim
[Display Python help in Vim](https://www.cyberciti.biz/faq/how-to-access-view-python-help-when-using-vim/)
  

### Python setup

#### Virtual Machine

* Console: [https://labs.alta3.com/tmux/napya-401-bchd](https://labs.alta3.com/tmux/napya-401-bchd)

* Static: [https://labs.alta3.com/static/napya-401-bchd/](https://labs.alta3.com/static/napya-401-bchd/)

  

#### Shebang

>  [StackOverflow Reference]([https://stackoverflow.com/questions/22222473/shebang-doesnt-work-with-python3](https://stackoverflow.com/questions/22222473/shebang-doesnt-work-with-python3))

```

#!/usr/bin/env python3

```

  

## Day 1

  

### Labs:

* up to lab 9 skipping 1-3

![](https://ssl.gstatic.com/ui/v1/icons/mail/images/cleardot.gif)

### I learned:
* String formatting with lists
```python
>>> octets = [192, 168, 0, 1]
>>> '{:02X}{:02X}{:02X}{:02X}'.format(*octets)
[output]: 'C0A80001'
```
also
```python
pets = ['Max', 'Garfield', 'Spot']
fish = ['Goldy', 'Finny']

pets.append(fish)
#print(pets)
print("I have 3 pets named {0}, {1}, and {2}, as well as 2 fish named {3[0]} and {3[1]}.").format(*pets) 
```
[output]: I have 3 pets named Max, Garfield, and Spot, as well as 2 fish named Goldy and Finny.


https://labs.alta3.com/?path=view/napya-401-bchd

## Day 4
### Lab 34
* https://test.pypi.org/project/example-pkg-jacedeuce/0.0.1/
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDc3NDkwMDk3LC03NjE3NjQ4MDAsLTEyOD
Q3MTEwOTAsLTQyOTk4MDU2MSwtMTE3NjM3OTgyNCwxOTEwNjk5
NzQ0XX0=
-->