**ip address of the machine :- 192.168.110.235**

![](attachment/87f2dcd2404bdae4d563db4cf5691a64.png)
pinging the machine to see whether machine is running or not.

![](attachment/fcf438c105ad474beba39a2a3e9f5a5a.png)
After running an nmap scan we found that only 4 ports are open out of all.

![](attachment/d6bd41e1e96a71cd1a5c9564d8787163.png)
Did a script scan like versioning and os detection. So, 55006 and 55007 is running POP (Post Office Protocol) as a service. There are also some command listed which we can use in the nmap scan.

![](attachment/97cf895d9c95a212b0a43de752fd6e84.png)
it was running web server so went to the website just to see it. Now will run gobuster and nikto further to gather more information.

![](attachment/48cd406b7ded571258fb2863bb252a71.png)
didn't find anything interesting in the results of gobuster.

![](attachment/3247c26037fee270c6b4edcc5e40b223.png)
**Apache outdated** server is running, **"cobalt qube 3"** is running on **splashadmin.php**, **apache default file found** and nothing else from nikto.

Now let's go to the website and start inspecting source code manually.
![](attachment/9e21f0137d42cd969da7f3062b053605.png)
terminal.js file might contain something interesting.

![](attachment/6fcddc365799d2ed5800b5b92e60ba16.png)
In terminal.js saw some comments, and came to know that user name "Boris" has a password and is encoded below so will now try to decode the password. "natalya" is also a possible user name but with no password. 

![](attachment/2f2b8b289dd155814cc56867d5c79404.png)
went on cyberchef.io and it decoded it from a form known as **"HTML Entity"** But password was wrong so used burpsuite decoder to verify it and then got right password.
![](attachment/28d8fe4072ef84e48fdf6e1f1dc435c8.png)

possible username:password found
boris:InvincibleHack3r

![](attachment/a2cf82008416ad877faecbb5d7c9877b.png)
We were able to login with above username and password and was able to access all videos and photos on the website.

![](attachment/54cfead8591d7297bcce410309883062.png)
So was unable to further get anything about the website through gobuster, nikto and seeing source code. But they gave hint about POP3 and we know that they are running POP3 on unknown ports known as 55006 and 55007 and 55006 is running POP3 with SSL and 55007 is running POP3 without SSL so we tried to connect to POP3 service directly through netcat.

![](attachment/26e452a5759f22a2d1feb2b83bbf7bce.png)
we failed in authentication which "boris" is not reusing password. So now, we have to brute force the password using hydra.

![](attachment/6b57b90e5b58805795a055c782d798c1.png)
got pop3 service password of boris.

![](attachment/b987ffd1b8fe9e791bcab899c770e35c.png)
We logged in as boris and can see he has 3 mails. Let's see them.

![](attachment/ab1b1246e4a85090d836204681e6f13f.png)
First was from root.

![](attachment/c46b1e1cf1048f9ffd7af3a2e88f0cf2.png)
Second from natalya which is again a possible username.

![](attachment/c6949d41c487ed6d46fed26798ec558a.png)
Third from Janus.

Natalya is also an employee like boris so let's try to crack her password as well to see if we can find something interesting in mails or not.

![](attachment/d1b9e33123935e76622aadba9348c789.png)
Found natalya's password as well.

![](attachment/2639e1077a97fe07acb18e7fb6cef2cd.png)
Didn't find anything interesting in her first email.

![](attachment/9157de624d63dd2f743ae8a0444f4933.png)
But in second some interesting creds. and a domain. Let's enumerate and test further now.

![](attachment/c485e7b967685807761fcd358d646ec3.png)
add domain and goldeneye machine ip to /etc/hosts file.

![](attachment/9a4e8c1de49201fabbc4fdbad5097c42.png)
This will open after going to the provided domain in email address.

![](attachment/82c6988145188b6995b0e17f6d596510.png)
was able to login on platform using creds.

Exploring account
![](attachment/f1c2094fe72f42f1bad14cf63f1960ce.png)
Found this message from Dr.Doak. We got his username, so may be he also uses pop3 service and has some interesting mails over there so let's brute force his password as well.

![](attachment/0929378fa170aa3138e24b81eb50d6fd.png)
Found creds. of doak.

![](attachment/582168296f75ab92b7398a78029946a8.png)
Found an email and found creds to moodle platform for Dr. Doak.

![](attachment/7577f26d61aadcd48c142c9d69d9a518.png)
found something in private file of Dr. Doak

![](attachment/6281fc088beaadbb36ddc50cc8d18263.png)
Found a file there and this is its content.

did strings on the image and found some creds.
![](attachment/f1c04a71133a78f24f35ac069061f52a.png)
In s3cret.txt they captured admin creds so may be they are admin creds.

![](attachment/1f7e74cba65245fa1e93718bed147167.png)
so able to logged in as admin with above password on moodle.

![](attachment/12aa8fcb4786357e988c45ba7943459a.png)
we also found some other users as well on moodle. Now we will start investigating all the options in the admin's room.

![](attachment/6de21f959d33512180679d3897f46a50.png)
In site administration -> Notifications we found that moodle is running 2.2.3 version let's see if it has some known exploits which can help us gain reverse shell.

![](attachment/3fd845e81e736cd7efcd0f56798f74c1.png)
saw this exploit on exploitdb and understood the comments and code and then saw that if i convert spell checker to PSpellShell and then change it's path in system settings to a payload to get reverse shell.

![](attachment/23e8bafabea099d1c65a16d220859061.png)
add this payload in path to aspell.

go to site pages and site blogs and enter anything and click spellchecker to get reverse shell.
![](attachment/f88079f9c48478f32fcec0638b934ebe.png)
got reverse shell!!!!

![](attachment/17b014f990c18d715cda98123a81e43d.png)
running privy.sh script to get some knowledge about the system. 

![](attachment/666649527d01fdd27fa442aca9d0c419.png)
let's inspect each file.

from cronjobs file didn't find anything interesting.
from mysql find didn't find anything to escalate privileges.
in network info file port 5432 is open but why?
![](attachment/ba5d84cff598bd74405560faae8d13b4.png)
in PathInfo.txt found nothing.
in Passwd.txt, root and postgres are running bash.
![](attachment/f755455372870c9f5ddf1de2be53a140.png)
in RootServices file didn't find anything weird.
in SUID-GUID found a file by name .htaccess in moodledata directory. No SUID and GUID binary worked for priv esc from GTFObins.
![](attachment/b428588823b8adb6f463a93b4a02e74c.png)
in Shadow.txt found nothing.
in SysInfo.txt, found some info about versioning and kernel version etc but nothing worthwhile.
![](attachment/62bae708c7c8101e03942d65daada5e0.png)
in UserGroupInfo file, got some info, which are files in all the user's home directory.
![](attachment/412010e9d963e40f463c3d085bfdd0a1.png)

Now if we didn't find any flaw/vulnerability that can help us escalate privileges so we have to search for kernel exploits or see whether kernel has any problems or not.
![](attachment/06c22ce098c2002990389eb21fc37f3d.png)
Got a lot of searches on searchsploit.

![](attachment/509c2aac1c0cce11aafee8fd86247a90.png)
got almost two exact matches. Now, let's decide which one to use.

![](attachment/9e315def2899ec72a0cf0e18d8838650.png)
So will be using 37292.c.

to run this exploit change gcc to cc so it will call cc compiler to run instead of gcc because gcc doesn't exit in machine.

![](attachment/e65aa0ed4f5cbb1715636de195b902a0.png)
Downloaded exploit on target machine. Now do "cc 37292.c -o exploit.c" and then simply run the executable.

![](attachment/5f07965ede272a97ed14b9f80550a43d.png)
Here, we got the root access. Finally, escalated privileges.

![](attachment/be6e12384d9988c95a9da3eda0e65a5d.png)
So, here we have got the flag..............