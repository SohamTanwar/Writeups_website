**ip of the machine :- 192.168.122.90**

![](attachment/3da0cfd0837524d77a55f2907eff8f9d.png)
machine is on!!!

![](attachment/46213ac4245d220d5e47c3c5e86239a4.png)
Found some open ports...

![](attachment/c2c216ef3e82a59c5765c383fe3296e5.png)
Performed an aggressive and found versions as well as one disallowed entry in robots.txt as well as domain to put in /etc/hosts.

![](attachment/cf975635ed0780296ffb96c1ea402436.png)
Website...

![](attachment/b69cf893ae3cd62adf21fd7add4ac8c0.png)
In website footer found that this website is made in wordpress.

![](attachment/37b8c32dfce4c7e3555573995cc24487.png)
Let's explore this directory.

![](attachment/aa51e4845564ff1f4e7a7b3bbb63f406.png)
Oh!!!

![](attachment/00010e3887d66c4eff52767f6b106c31.png)
Just found a bunch of directories of wordpress. Let's use wpscan.

![](attachment/3936f78b961cb56c83b0c035a3f57b98.png)
Found two users with wpscan.

![](attachment/d95749a4504e61bc889d639c27fd13b8.png)
So, tried to brute force the ftp service and found the password.

![](attachment/5d1d7afc21d75e85ab40e4cf59ab9530.png)
Found a file, let's view it.

![](attachment/efbaaa728a2b5e34745949fcd2db4bdb.png)
Oh!!!

![](attachment/0b77211423994e2e69c6edf5f87862c7.png)
Tried the same creds. and got initial access to the web server through ssh.

![](attachment/64b02c8c7e13e972eeb61574e35a4f24.png)
rbash restricted. Let's try to escape it.

![](attachment/aeac0209454a9f6d0654ddadd30f7f4b.png)
So, came across a blog and escaped the shell.

![](attachment/31c323ebe211bc78623726c9b9f50444.png)
So, found a .tar in user funny's home directory and a .backup.sh which is compressing the /var/www/html directory. So, got the html.tar in my system and extracted it. Let's see what it contains.

![](attachment/2a21e3adeb46586a4e5b94310d9c1bd9.png)
In, wp-config.php file got creds. to the database.

![](attachment/d7fea23bf213e07f0517fb225b55c9e2.png)
So, creds. didn't work. But we can edit  .backup.sh file.

![](attachment/d662eebc1a47f9447ba18badd65daa74.png)
So, added a rev. shell payload in the file.

![](attachment/e99b5ee744343371f8488ce542bd4250.png)
It was a cron job so got the shell.

![](attachment/c3bc902da201799fc2c920e576cda2f2.png)
So, i read a person's writeup and he said that the cron job is running as both root as well as the user, so got root.

![](attachment/b9ac4b03b414277c328ae5402172d31a.png)
Got it!!!