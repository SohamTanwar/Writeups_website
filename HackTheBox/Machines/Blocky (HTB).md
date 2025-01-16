**ip of the machine :- 10.129.6.133**

![](attachment/f5b99937dd4bca19425f04fafbf98547.png)
machine is on!!!

![](attachment/b59f93542f415a90acb308529a06b74d.png)
Got some open ports, got a different port this time... Minecraft.

![](attachment/7b27f6fd9f1db6be21e0f8c4f9e74db5.png)
Found versions of the services running on the ports except FTP which i am expecting to be either ProFTPd or vsftpd, it can be only one of them as they are the extremely common FTP services that can be run on port 21.

![](attachment/6e52140f49481569f5e9400f25950fb5.png)
Add ip with domain name in /etc/hosts file to access the website.


![](attachment/f81bce23d42c65818cbe5751b468c670.png)
Seems like the developers are working on their own minecraft web server that's why port 25565 port which is the default port for minecraft server.

![](attachment/8157dfe2fcca5369c3ac7310ca306f6a.png)
Found a blog post and seems that website is running on wordpress.

![](attachment/5ad54c0e1a495f8f638b6e5a355d1b18.png)
Clicked on blog post and found the author name "notch" which is a possible username.

![](attachment/667c333ef341b958a13206392a343e18.png)
Found some possible directories. Let's explore them.

![](attachment/e7031e93815e4ca31062ce77e884a168.png)
found a phpmyadmin login page...

![](attachment/3e7051773da45518a87ebdeb86463e37.png)
let's try some default credentials.

![](attachment/0c66b2044187ba88d43f98cba7c94d0e.png)
it didn't work, let's move to next directory.

![](attachment/a13e0f9bf70b7c17285b6318a17d2fbb.png)
Found two jar files in /plugins/ directory and downloaded them, let's see what they contain.

![](attachment/297386bc78149bd5db1b3532a08c86c4.png)
downloaded the .jar files and extracted them using "jar xf" command.

![](attachment/386b1301aa3d5ceddc783d39b0a0fce6.png)
in com directory and further sub directory found a .class file.

![](attachment/a3a5d023b10039804f4f756e8798dca9.png)
Viewed it's contents a bit gibberish though but found something under root.....
(8YsqfCTnvxAUeduzjNSXe22)

![](attachment/1efa67fccd33cd9853f05ded519afe2d.png)
It's not a hash so possibly a password i guess...

![](attachment/6c6294e393f4cdfc6ca3b715424bd729.png)
used the password with root and was able to get through phpmyadmin. (root:8YsqfCTnvxAUeduzjNSXe22)

So in wordpress database and further wp-users table, got a password hash for user Notch.
![](attachment/c944bfa02adf93009681118f39e6169a.png)
Let's try to crack the hash.

![](attachment/f9481736407df36a465a72529dadba00.png)
Also found hash type, let's crack it.

Was unable to crack the password through hashcat maybe the password is too strong so hashcat cannot crack it from rockyou. But the only password i have found is of root user of myphpadmin. Let's perform password spraying.

![](attachment/e6836d39255e9e5170b51532691868b7.png)
So directly tried to login through ssh and failed now let's try to login through ssh as user "notch".

![](attachment/0116697f4c4e0d1c41c95f2b4eecea42.png)logged in....

![](attachment/ea28f5b13da8cb9544c256758c407f81.png)
got our first flag....

![](attachment/98d3ed2db0a575cb912c47a92321a1a0.png)
User "notch" can run all the commands as root user.....

![](attachment/ae4ec6925461f5c26f736251376ab5f1.png)
So started a bash shell as root user and got the last flag.....