![](attachment/e740d34cd6eb28f77091ae73863ed118.png)
machine is on!!!

![](attachment/863c8ed10ccca98c97ca7526894a1ab3.png)
Had to add ip and domain name in the /etc/hosts file because it was redirecting over there.

![](attachment/8e75063a32e57a91ab28da78c6da7c04.png)
only two ports open on nmap scan.

![](attachment/1d88fdf03e622fa0f5c98a3b5f86fd82.png)
did a script scan and found nothing interesting.

![](attachment/238b10bd5eac67f3eb3345297f58ce2a.png)
found some directories to look for.

![](attachment/97b7b01bf5deaaeb6dad3ae327962d60.png)
Didn't found anything in those directories so did subdomain enumeration and found one.

![](attachment/178a6e09175e768d234d7740b3acfcd3.png)
Also add this domain in /etc/hosts file.

![](attachment/ae88da1568f267a87a10aa675cbe1686.png)
Added creative.thm website to see what it gives and showed a normal website.

![](attachment/d4b1c0ca1f3e7f6ab843e7e62b1eb3ea.png)
But when added my ip address with port running a web server it gave my directory listings this means we can do command injection with specified port to get some information.

![](attachment/2f814dc68ed95122ee8fcb1a3e8cf6bb.png)
After modifying the url data we are getting the output as "Dead".

![](attachment/95f09c88b4ebf5f7211e8ef7f06232b8.png)
In intruder brute forced the port to get some more information and in payload chose top 50 most common ports.

![](attachment/b0437729c54069a711f91de8f68cdc2a.png)
All ports gave same content length except port 80 (creative.thm website) and port 1337 which gave out all the directories of the server. 

![](attachment/74f8c99bdaa0d0a33caad498f40d251b.png)
port 1337 gave this.

![](attachment/decf815d76da57aed2132f2c29eeec16.png)
/etc/passwd file revealed a username named "saad" with a home directory. Let's see if we can access it.

![](attachment/8b295f8a8eabc4b2df6a91feea647e28.png)
was able to access his home directory and gathered a private ssh key.

![](attachment/03c9fd9b69745af587d94882fa6c2361.png)
the ssh key is protected by a passphrase, so trying to crack it using john.

![](attachment/0c3f5db1110e71df843f97312d11804d.png)
Found the passphrase.

![](attachment/bcfde6543bb29031adfe1eae1871b402.png)
Found 1st flag.

![](attachment/40463e129fa97b1f540aadfdb0100498.png)
in .bash_history file of saad found his password.

![](attachment/e96ba2c20a4565700fec04cf41167fec.png)
did sudo -l to see what permissions do saad has. Now didn't find anything on GTFObins related to ping command for local priv esc. But from an article found that LD_PRELOAD is an env variable which is used for listing shared libraries with functions that override it and can be used for local privilege escalation.

![](attachment/86b2d8b50e4c58bc983f0d215c652abb.png)
in /tmp created a C file and added this code in it.

![](attachment/968389959723f979441ec51c9406c0e3.png)
after compiling and setting exploit to be the value of the env variable. Used the env variable with the command user was able to use which is "ping" such that the exploit override it and gave us root privileges.

![](attachment/8226a91c835941ef8ac8edad685fa42a.png)
got the last/2nd flag........................