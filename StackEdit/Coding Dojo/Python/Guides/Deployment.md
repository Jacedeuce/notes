1. create repo
2. add gitignore
3. commit files
4. pip freeze > requirements.txt
5. go to AWS and create ec2 ubuntu 16.04 ssd
6. allow tcp ports 80 and 443 in security groups
7. create and download key pair
8. launch instance
9. connect with ssh in folder with .pem



### notes from deployment
* path to static_root didn't work with my templates directory - had to change dir to "static_root/"
* swap username from `ubuntu` to `cloud_user` 


#### nginx
```
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2019-06-21 23:36:46 UTC; 6s ago
     Docs: man:nginx(8)
  Process: 2703 ExecStop=/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid (code=exited, status=0/SUCCESS)
  Process: 2716 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Process: 2705 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
 Main PID: 2717 (nginx)
    Tasks: 2 (limit: 2361)
   CGroup: /system.slice/nginx.service
           ├─2717 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2719 nginx: worker process

Jun 21 23:36:46 jdhanna1c.mylabserver.com systemd[1]: Starting A high performance web server and a reverse proxy server...
Jun 21 23:36:46 jdhanna1c.mylabserver.com systemd[1]: nginx.service: Failed to parse PID from file /run/nginx.pid: Invalid argument
Jun 21 23:36:46 jdhanna1c.mylabserver.com systemd[1]: Started A high performance web server and a reverse proxy server.
```

[Workaround]
```
sudo mkdir /etc/systemd/system/nginx.service.d  
printf "[Service]\nExecStartPost=/bin/sleep 0.1\n" | \  
sudo tee /etc/systemd/system/nginx.service.d/override.conf  
sudo systemctl daemon-reload  
sudo systemctl restart nginx
```

##### Now:
```
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
  Drop-In: /etc/systemd/system/nginx.service.d
           └─override.conf
   Active: active (running) since Fri 2019-06-21 23:39:57 UTC; 7s ago
     Docs: man:nginx(8)
  Process: 2761 ExecStop=/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid (code=exited, status=0/SUCCESS)
  Process: 2775 ExecStartPost=/bin/sleep 0.1 (code=exited, status=0/SUCCESS)
  Process: 2772 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
  Process: 2762 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
 Main PID: 2774 (nginx)
    Tasks: 2 (limit: 2361)
   CGroup: /system.slice/nginx.service
           ├─2774 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2776 nginx: worker process

Jun 21 23:39:57 jdhanna1c.mylabserver.com systemd[1]: Stopped A high performance web server and a reverse proxy server.
Jun 21 23:39:57 jdhanna1c.mylabserver.com systemd[1]: Starting A high performance web server and a reverse proxy server...
Jun 21 23:39:57 jdhanna1c.mylabserver.com systemd[1]: Started A high performance web server and a reverse proxy server.
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5MzcxNDkxNCwtMTM4NTg2ODU0OSwyMD
QwNDEyMzcxLDczMDk5ODExNl19
-->