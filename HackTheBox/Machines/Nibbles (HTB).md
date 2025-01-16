**ip of the machine :- 10.129.3.31**

![](attachment/f8916fe7953a7a7fe7d444bf1d3bf3c6.png)
machine is on!!!

![](attachment/4dd73a7c9134a7beadbc11c9c5c86627.png)
Found two open ports as usual.

![](attachment/7b7ca1a3fe1738b689c059e802be7759.png)
got version of both the services running on the ports...

![](attachment/224b8fea14feac52aa777a179cdee974.png)
Added ip on the browser and got to see the web application with only hello world.

![](attachment/6116cf73b9f0ec738ac6d3d12b9dcb7d.png)
So after viewing the page found a directory, so let's view it.

![](attachment/5001a7d51281c4b2629ab6ff0f714dc1.png)
Huh!!! Powered by nibbleblog, but what is nibbleblog...

![](attachment/0fd2c465fc09c0edec4a6a519f22cb3a.png)
So it is an easy, fast and free CMS blog management kinda thing which is no longer maintained...

![](attachment/99945ad57b30f42fdc117401a62b5ea3.png)
It's src. code has a lot of php files which is a point to be noted...

![](attachment/d604648d1715c28038e625cf91964be8.png)
On directory fuzzing with ffuf found some .php files and directories.

![](attachment/21bf720b7d750beb97be7702ddfdee97.png)
found a login page.....

![](attachment/00e2598c7d94103c29a303e170532343.png)
So logged in with creds.... (admin:nibbles), got an idea of username as admin from some searches and nibbles as password is what i randomly guessed!!! Just pure manual brute force...

![](attachment/aac6f0df00e061963d7e5f3d2aaa65f2.png)
Found only one exploit only.....

![](attachment/6eccc9a1b167e428fb2aa2ffe1fa8b45.png)
So ran the exploit with a payload as php reverse shell by pentest monkey.

![](attachment/7e1a132b08e944f30c36078d35494351.png)
got rev shell....

![](attachment/0c09c168c03a53fb1f66888294efb6e9.png)
Got first flag!!! But also got a file personal.zip.

![](attachment/b1aa9509c5738b7916bdd9e277f99e44.png)
A file in directories!!!

![](attachment/f21f4920ee15f6252c5563ef4580c51e.png)
A script but can be run as the logged in user only.

![](attachment/5b2081b52cfc5135547be7a24dc8c21b.png)
We can only run the script as root user and we can also rwx as normal user which is easy priv. esc.

![](attachment/268e9fdd2ddc2eb08f26f86f3b7ac529.png)
So added the '/bin/sh' in monitor.sh and ran the script as sudo and got the root shell...

![](attachment/94e8936bc439baaf579daf07a386f997.png)
Got root/final flag...