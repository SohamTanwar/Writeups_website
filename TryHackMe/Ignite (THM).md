**ip of the machine :- 10.10.81.225**

![](attachment/93d462bf1c24f88984cdfbef1e906eb2.png)
machine is on!!!

![](attachment/88e5fd2dab4d2012ff8d515a670ebb44.png)
oh!!! only one port is open.

![](attachment/55da7fb5adea76c302a33e3382dc25b7.png)
so it is using fuel cms which is also based on PHP.

![](attachment/10420b7bf3fdbb67d0148b92634dba4f.png)
in src. code found the link to fuel cms on the web server with creds. hardcoded "admin:admin" in src. code itself.

![](attachment/8f22076b7582037eafcfde86180377dd.png)
we known creds. are admin:admin.

![](attachment/46e3a46b7af756d3bc32caa476de7b66.png)
got in!!!

Let's search for any possible exploits.

![](attachment/d065402a7ca92bedc526e46d4eb7cf00.png)
Found this exploit, will try to use it.

![](attachment/0f30e2d9f76121192bda74b546bc9980.png)
ran the exploit!!!

![](attachment/aca2e67057f53d3d6e307deadc05016a.png)
got rev. shell.

![](attachment/1ea787ad04fa684af464779870fab67b.png)
So there was a user in the home directory, in which we found our first flag.

![](attachment/394856ce9560a5f7cc1418fd85ceaa7b.png)
found some SUID binaries and libraries but was unable to escalate privileges with any of them.

![](attachment/3eea42e42c9d8e3624e6caff2e49ef85.png)
in /var/www/html/fuel/application/config/database.php found creds. to access database.

![](attachment/b03e9050235c1938900caf414a461383.png)
into the database... But no luck.... Didn't find any way to escalate privileges. 

![](attachment/96ac2ef0ccc6aa5fd7d11e15c888992c.png)
So i tried to do password spraying which is if root user using same password of the mysql server as his own as well and was right.

![](attachment/2186ce87ee7c810dbe3c31fdcb38845c.png)
Got the last flag.....