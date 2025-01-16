**ip of the machine :- 10.129.229.118** 

![](attachment/fc1d809f68bd0161ffb173f4361497c2.png)
Machine is on!!!

![](attachment/235430b108535e23fc9805550c909489.png)
Got two open ports!!!

![](attachment/f99f68ea56688108aaa654e6b7be36ef.png)
Got versions to all the open ports and also got one disallowed entry from robots.txt.

![](attachment/e0252391b37095d0bc8e6f30b84f5154.png)
Saw just a normal web page.

![](attachment/8bbc0c0b0035f3601a995bf51dbfa26c.png)
Again in /writeup just a normal web page.

![](attachment/c2804ed4a103c7268945f66b821488f0.png)
In src. code, found that it is made in CMS Made Simple.

![](attachment/7cbcf323b34aeee375feb570aaebdf6c.png)
Found one exploit with associated CVE.

![](attachment/474a68065632a5e5e2e71226914106f0.png)
Ran the exploit and got some hashes let's crack them.

![](attachment/afb6a0cc530b35c5099ff7bd789202ed.png)
Cracked the password using hashcat.

![](attachment/4b3fa71a125a8c8f710ac2e66fac5f50.png)
Logged in as the user through ssh and got user flag.

![](attachment/986cc96c6826806988d7fb3e9c310db0.png)
When sshd as the user, root user runs /usr/bin/env with sh and also specifies init directories.

![](attachment/b704289cb58c701197aabb63693c785e.png)
As the user is in the staff group and directories in /usr/local can be write by the users in the /usr/local directory.

![](attachment/68d06491bcd39610384075796ca044db.png)
So made a one line and added it in a file in /usr/local/bin, so when logged in again through ssh it will give /bin/bash SUID permissions.

![](attachment/a0f4d20a5766e9c821d23758e1e2d523.png)
It gave it SUID permissions and got root flag.