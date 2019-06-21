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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODU4Njg1NDksMjA0MDQxMjM3MSw3Mz
A5OTgxMTZdfQ==
-->