**ip of the machine :- 10.129.229.183**

![](attachment/ff898459d5dc43931779a2020207c554.png)
machine is on!!!

![](attachment/d4626b95ac952bc5826d7ec8da8458f9.png)
Got a lot of open ports....

![](attachment/415cabd058a632065ba780e6ff6c8d06.png)
So only port 22,80 and 443 are only of some use... Rest don't know but will be looking for http and https for now.

So website was not loading so went to official HTB writeup of Beep machine and fixed it.

![](attachment/9d136a629dad43977f1fe339d1d3e9f8.png)
Now can see the website and something called Elastix but what is it...

![](attachment/5b22e08af270290bb80555355584004b.png)
So found defult creds. first so let's try them... and it didn't work..

![](attachment/f82b97b3d2dc01c6cffd3cab7a5ec9bf.png)
Then observed my nmap scan again and found another http server running at port 10000. Let's visit it...

![](attachment/184e0338ca4cd82a4424877f7c090619.png)
It is running webmin....

![](attachment/9e994c2d6a76e134c024b204240354e0.png)
Webmin default username is root and password is system's root password... So it is of no interest right now.. Let's look for any exploit of elastix.

![](attachment/ec6a05e9d628e662d06586d9653a3959.png)
So did directory fuzzing and found a lot of directories..

![](attachment/3a854f2c73174f4200c080dad20d6a33.png)
Can see configs directory but cannot view the files... Same with lang, libs and mail directory, found nothing promising.

So after going through all the directories, found one that was interesting...
![](attachment/c9cecc48f88f0867cb7d58071b51aa36.png)
Found a crm and also it's version which is 5.1.0, let's find a exploit for vtiger CRM version 5.1.0.

![](attachment/3a831cd32dc1d4d47c826197dcfc713c.png)
Found an exploit which says that vtiger crm v 5.1.0 is vulnerable to LFI. Let's add then payload provided then.

![](attachment/f7e4b980e3117c507b0d30fea07839c4.png)
Added the provided payload in the exploit and can see /etc/passwd file.

i was unable to figure out how to do LFI to RCE, so went hunting and found another exploit..
![](attachment/68439939ef94b56f243616c03bf9a8ec.png)
Elastix 2.2.0 but the payload it provided was, 
![](attachment/57dd50352c6d07d882f36556610f1930.png)
of vtigercrm, so let's try it...

![](attachment/6e89b7161f23259570498241888dc1b7.png)
So after adding above payload can see a .conf file which revealed some creds. 
![](attachment/81529d724f4c6f2de37e6d210036727d.png)
So digged some info. about amportal.conf and found that this file contains some intial configuration about the system and specifically about the Asterisk Management Portal...

![](attachment/4f62d19fa151c0d00a59ae361dbab8fe.png)
So was able to log in as user root directly by performing password spraying as the password used for database and ssh login through root user was same.

![](attachment/9796bf0a24b6fed6488d9b5e8669d3f9.png)
got root flag first.

![](attachment/60d895e2c91de07fbfd2bcc48015a6e4.png)
Also found user.txt file.