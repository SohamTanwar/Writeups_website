**ip of the machine :- 10.129.29.200**

![](attachment/a7f82df5ec0be95446e6430bed867822.png)
machine is on!!!

![](attachment/ad42bd4ec9717e4f439f90b45d409ed9.png)
added ip with domain in /etc/hosts file...

![](attachment/f170b4f4ced79179e1f36aba161f46a6.png)
Only three ports are open, 53 is for DNS, and 22 for ssh and 80 for Http, because 53 for DNS is open that's why added domain with ip in /etc/hosts file, else site won't open...

![](attachment/bef6c9be78e97092411899c2c53fcfe4.png)
If we write ip in the browser this will show up...

![](attachment/28a050de137cc150c936833baafccbe4.png)
If we type bank.htb it will show us bank.htb website and to be specific login.php, let's do some directory fuzzing now...

![](attachment/a9ddb1c4a925a5139055516cd4751b15.png)
First did a common php file names one and found that after visiting any oh the above it is redirecting to login.php. Did a php files scan because it redirected to a php file.

![](attachment/e4627ea90ed35eec09e654968ab949ed.png)
So after using lot's of password lists, for directory fuzzing, directory-list-lowercase-2.3-medium.txt from seclists gave the directory which looks interesting...

![](attachment/429392e95f96026c675ee17fc3f181de.png)
Went to the directory and got some .acc files, not WTF is acc huh???

![](attachment/e61545ceb2c848ed16e2633dc2906f32.png)
used in accounting which means details of users...

![](attachment/4b06be6f238509b0e1812a22a7ac30b3.png)
Downloaded any one and saw what is in it and got an email and password. So basically tried everything and found nothing and it says it is encrypted and saw one more thing that there are many .acc files so let's see what other files have...

![](attachment/8c4c25ef1932109e936ffb6b7459ba9a.png)
Found a file with size 257 which looked unusual so downloaded it and open it!!!

![](attachment/4d2f88c17ea17f371f1d8ad229d28b32.png)
got some creds...

![](attachment/f704dd362d68a4a77fe0c4cc526bed11.png)
Entered some creds. and now authenticated.

![](attachment/698226ad655568371199ea9262cd99a2.png)
So now went to support.php and saw that we can upload something...

![](attachment/644e23b12bc62261fde4456eac62d181.png)
Found this in src. code which means if i upload a .htb file it will get executed as a .php file.

![](attachment/c0a5b649c2bc72645958911841daf874.png)
added the ip in pentestmonkey rev shell and renamed it with a new extension.

![](attachment/6ed7336e3a915c4d735fa4cf18f0e494.png)
So chose the file and submitted it...

![](attachment/96d16fdd2af7dceb61d881221917c6d1.png)
it is submitted now and then clicked on attachment and got rev shell...

![](attachment/0bd99ca764a8612c7c06f728d14ecd08.png)
Let's see what we can find...

![](attachment/0fea64d28821aa4f74b5fd28e550a56f.png)
Found a user in /home directory and can view the user flag...

![](attachment/5a24eb2e65cf722accab02dd7d67224c.png)
Found SUID files and first one seems strange, /var/htb/bin/emergency.

![](attachment/ec3a9484ff2f881e686d3fad64bb38fd.png)
So just ran it and got root...

![](attachment/06a25cdfe7c8e8e5911970b7748ec8cb.png)
Got root flag...