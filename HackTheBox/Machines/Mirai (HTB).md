**ip of the machine :- 10.129.214.193**

![](attachment/42a7aaa890062140b3955ef715ebf254.png)
machine is on!!!

![](attachment/e924c9d2b9a9bdb204731a38c53de976.png)
Wooh!!! A lot of ports!!!

![](attachment/fa7092823adab5e931fb440e1d42d4bc.png)
Let's see port 80 first...

![](attachment/dd3056dc204078ec7e21a5fb1cf443c2.png)
got nothing... maybe index file don't have any html code i guess, let's do directory fuzzing then....

![](attachment/cafef6fddc46c9384b8e5d3839425c4a.png)
Found only two dirs. first one looks a lot interesting though.

![](attachment/bb3002f2b14f0eb7a1b2b2dbd8be61e1.png)
Found an open admin console.

![](attachment/9f4c37508ba50648cb4753c9b91b319d.png)
found a login page...

![](attachment/a868770720cf939aad86215cc196ebc3.png)
found pi default creds. but are for raspberry pi.... Then searched raspberry-pi vs pi-Hole.
![](attachment/10e8ae281a1bb82855c50e17aa7f6143.png)
So pi-Hole is basically raspberry pi but for docker.

![](attachment/16c91b91462dc97c64374e72ba2585cc.png)
So using default credentials was able to login to the server using ssh.

![](attachment/ba128882d1f24001f7ba6d8ec16fd73c.png)
No user.txt but we can see the .bash_history file this time... Let's see it then...

![](attachment/aea0a379bf11e58fe16f30c36c3cb5e6.png)
user pi ran "sudo su"... well does that mean our user "pi" is the root user only.

![](attachment/47f42468786edd90baabf311db124b46.png)
was right abt it...

![](attachment/f4761c390b5b6cae766f42315542a256.png)
privileges escalated vertically.

![](attachment/2aa6e8909da10d54145dfd90a52be6cb.png)
got first flag in "Desktop" directory of the user "pi".

![](attachment/6d991e0dfe25b30d374f9f089e9605e3.png)
root flag is not there, usb stick...

![](attachment/a26a37b90fb67426dc8c9628622faa3b.png)
Did lsblk to see all block devices and found usbstick...
/media/usbstick.

![](attachment/cba605488a77489a25d0c10bfd912313.png)
What the hell!!! deleted files of the usb stick...

![](attachment/3e94b05fc0a90a02150d1d1a13c3f520.png)
So tried to get to the mount point and found that it is not a directory which means a file...

![](attachment/bb3efd1aec28dc61fdfd62e03cdbbe70.png)
it's some kind of binary file, so let's do strings then.....

![](attachment/f6aa72afa597d4980535e6869f7194db.png)
Got our last flag!!!