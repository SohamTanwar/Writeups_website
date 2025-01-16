**ip of the machine :- 10.10.18.188**

![](attachment/8088f7c4c9f074f14a7d38582c9d15e2.png)
machine is on!!!

![](attachment/f6e7412c9796d582764ea005d87dd0af.png)
Got two open ports!!!

![](attachment/0874e2b8b8c55175ecfb638b9306c055.png)
Did an aggressive scan and got versions of the services.

![](attachment/8b9ca23d5c573fc8a9c759b8dcf5985c.png)
Just a normal website.

![](attachment/7af749f5b190950b89b692ae6688e505.png)
Let's add skycouriers.thm in /etc/hosts.

![](attachment/7a7d5f1bf2b4f0c2f9921149bf8296c3.png)
Added!!!

![](attachment/a9e9211d40345aaa3e7287f4e9e58b84.png)
Got some directories using ffuf.

![](attachment/e30b5bf360c00129e50cd59bb750619b.png)
Saw phpmyadmin but default creds. didn't work, but atleast now i know database exist.

![](attachment/73c4fd03cffbc4ddcb246202aad38cc8.png)
Got a login page. Let's register.

![](attachment/f33e8b6a5133d99ef7974a64e6f7a3e8.png)
Just created a dummy account...

![](attachment/28bfc016f06bcc25ee6ff5193b407297.png)
SIGN IN!!!

![](attachment/bd9c59ff16a324f5ead0e79b83272c39.png)
Got a dashboard...

![](attachment/78fa754c72aeb5e15ceead5cf5093791.png)
In profile section found email of the admin "admin@sky.thm".

![](attachment/03f0a60b9978bc0ac42dffc3c272f8fb.png)
Found a reset password page.

![](attachment/ecda7a89d9355ef1d3770946080e610a.png)
Observed the "forget password" request in burp suite. We can change the email id. Let's change it to the admin one.

![](attachment/48fcefafbee29d7b6d890385a8e7a683.png)
password changed of the admin...

![](attachment/089c1680acad5c14779e10765cac360c.png)
Let's try the new password.

![](attachment/215739e8dc5ba18365732173c1628e5a.png)
Oh!!! Logged in!!!

![](attachment/cb87af955d154be92bb940c56588630f.png)
In profile section we can upload our profile photo, so let's try to upload it...

![](attachment/8fd09ad04309cb34df73630d132523d9.png)
So, uploading pentestmonkey reverse shell...

![](attachment/88e1efecebfcd7aef74304f4947d6c58.png)
Now, when explored the response of the request after uploading, got the directory where our reverse shell would be. Let's trigger it!!!

![](attachment/8b86ae3827d2c14d7d8054f49164efea.png)
It's loading...

![](attachment/9bb3d57939c7e4efeaac2bd9634d3678.png)
Got initial access to the server.

![](attachment/c6e3476fec541b19adc512760c7b9172.png)
Got a user in home directory.

![](attachment/c42437b0106f8253d6e3b7f88812c374.png)
Got user flag...

So, now in order to login as user "webdeveloper" we can login into mysql and find the password of the user but there are no mysql creds. hardcoded in phpmyadmin and anywhere else. So, ran "ps -ef" to see background and found something strange...
![](attachment/724a3dd4d800596e950e934c34b879a6.png)
Mongodb is running...

![](attachment/f4a867dab0afa085a8c4f98613889d2a.png)
So, searched and found that typing "mongo" will give an interactive prompt to access the database.

![](attachment/5fd766a1c74a944fb569dec6b6073d9c.png)
So, found the password of webdeveloper user.

![](attachment/b74b2da8f11434804d0f35f6227f5430.png)
Logged in as the user.

![](attachment/571cc02af7bc1a075ab4bcdf7addf9ff.png)
Found some SUID binaries.

![](attachment/11aa4be89572a4b5de7652ba17d2d1aa.png)
pkexec with polkit!!! Found polkit and pkexec as SUID.

![](attachment/1693b51712126cea3e9fcf515f4c0524.png)
Also started another session through ssh...

![](attachment/38b2ebed8622c286829ca22ac4f06224.png)
in rev shell session, the process id is 1638.

![](attachment/92b60bb36dd01f82e88db55bb00d470d.png)
Started a terminal agent using polkit in ssh session with process id of the reverse shell which is 1638.

![](attachment/bfebc3ccfe44ed20149973635653264c.png)
So in rev shell session typed "pkexec /bin/bash" to invoke a bash shell and it asked for password in the ssh session because a terminal session of polkit is running which is from a process 1638.

![](attachment/afe84df305a47c215191b047b782acbd.png)
After entering the password, got the root shell.

![](attachment/6426536558c51303d67db1805cf93b95.png)
Got root flag!!!