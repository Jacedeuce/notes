## Task (in a single cli entry for each of the below):

#### Output “ls –la” of your ~ directory into cleanup.txt
```console
[cadmin@centos-08 ~]$ ls -la > cleanup.txt
```
#### Add a list of all files in the /var directory (and sub directories) that end in txt into cleanup.txt
```console
[cadmin@centos-08 ~]$ find /var -type f -name \*.txt >> cleanup.txt
```
#### Remove all repeat spaces from the cleanup.txt file and create a new file called cleaned.txt
```console
[cadmin@centos-08 ~]$ tr -s " " < cleanup.txt > cleaned.txt
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk0MjAyMDM3MV19
-->