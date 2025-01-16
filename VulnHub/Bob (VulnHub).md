**ip address of the machine :- 192.168.110.104**

![](attachment/8221cd680674dd5953a161fb7007ce44.png)
First pinged the host to see if host is up or not.

![](attachment/fcf24ae56eafafb56d2717f52b9b39c1.png)
Scanned for open ports.

![](attachment/0fdc9e1f6932498a65c38edf6c11f6ef.png)
For versioning got to know that some web pages are present that seem strange and ssh is running on non-default port which 25468.

![](attachment/4d0b5716e767d2663d2b7a4fb643b049.png)
From gobuster found that /robots.txt can be accessed directly so we'll see that after using nikto for other vulnerabilities.

![](attachment/49645362c5eb4543b375be0aa01f6a8e.png)
From nikto found that /robots.txt has three entries, /login.html can be used to login as admin and nothing else.

![](attachment/1cfd95ef21178e6832dbd26655626cd7.png)
Visited Website, let's look at the source code first.
Didn't find anything interesting in the source code.

![](attachment/06f360c7812b98b1e0b61ba22d78a2c9.png)
Only news one worked and here got some possible usernames.
Dean MacDuffy (Principle)
Alex Johns (head coach)
![](attachment/d0ea8a141bd9c10a00a3e40ed3eeaa75.png)
Got this in news.html source code, possibly base64.
![](attachment/43eb820e3ff6affa337fcfe010827ac1.png)
it was base64!!!

![](attachment/e7572ff9a6b8719a0cfd44294adfa4ad.png)
Found another web page.

![](attachment/db0e86caa92c3ff8eeae89b7e4dcb2bb.png)
Got a contact.html page as well.
![](attachment/590189227e2140c553a7be25e9ad64cc.png)


![](attachment/5d3e31e97c4cda23e79affe89247d5b2.png)
Found this after visiting /robots.txt

![](attachment/ae4418095ddf918e04948f3446e05459.png)
Visited /passwords.html first and found this.

![](attachment/891d883ce5054863722e055a438cecf4.png)
Another from bob and it seems bob is an IT admin or something from IT and he says a web shell is running and there has been a breach in the company recently.


![](attachment/da5d413b4b45ee68315ac834121749ec.png)
This means we cannot login externally.


![](attachment/4d4a99a1069f1afefe91f037116545bc.png)
This may be the web shell Bob is talking about and is unprotected which means anyone can use it.

![](attachment/b0dde4a60f7c14cc9a008815dabe6e3d.png)
only "id" command is working so let's use id along with other command in one line.

![](attachment/44daae3d246be74d0e9dacd8c5a35b05.png)
added reverse shell payload with id and pipe symbol to get a reverse shell.

![](attachment/c3ab78072d13276d6c6c7f1c1f09ec74.png)
finally got reverse shell!!!!

Now will run privy.sh in the machine to discover vulnerabilities and escalate privileges.
![](attachment/f7ab18691bd3614c824e52bde5a7d0ec.png)
Now let's further analyse files.
![](attachment/d33d2c4f06d4ee6a893a36dac2e104e6.png)
in CronJobs.txt didn't find anything and MySQL can be accessed easily as root with no password.
NetworkInfo file is just a normal file only.
PATH-Info.txt file contains just normal stuff nothing unusual.
![](attachment/ae7f9404adccc9cdf2ddd6ddf702a79b.png)
all users running bash as there shell in the system.
Nothing new in Root Services file.
![](attachment/f8626f2cf20a6bf566a1c4fc7b20ae90.png)
Got only one world writeable file in SUID-GUID.txt. But none can be used to escalate privileges after searching and trying acc. to GTFObins.
Unable to access Shadow.txt file.
![](attachment/2887e484679ec2d5cfb7c6e82b75761d.png)
Got some important sysInfo which can be used further for exploitation if we do not find anything further.
found home directories of every user and are just normal home directories and found a file
![](attachment/e8a8e11e808a47bfaacfbf8989a46f8f.png)
in a user name elliot's home directory and also one in bob's home directory.
![](attachment/a4a7ed4a02af3e28ebc741c6c8daf27e.png)
and was able to read both the files because we have permissions.

![](attachment/be49d8aa8bc28357447006be0bf768e9.png)
in this file elliot says that Sebastian's password is "Qwerty" which he suggested him.

![](attachment/ae32f30e19e9b8877166e96db6320842.png)
oops!! got some creds. finally in bob's home directory file. But sebastian (seb) has some pretty good creds though instead james has qwerty as pass.

theadminisdumb file says that seb and jc are new IT staff members and we know that an ssh port is open at a non-default port so let's those credentials over there.

![](attachment/4865999f226fdf36b7d47c1fefb25bd7.png)
with jc's creds. was able to login through ssh.

![](attachment/9017e9575922c8c7d376d2c2f1be14f8.png)
was able to visit and see files and directories in bob's home directory.

![](attachment/712877639ea2f2b43db9f225c1bbe0cc.png)
Found this executable and ran it. Boring huh!!!!
But if we take first letter of every line it creates "HARPOCRATES". And i though it is the password of bob but it is not.

![](attachment/706916adbf491c30b5d6bfc549bf5afc.png)
![](attachment/cbcc728995870ff0479813b3b67519f9.png)
we found login.txt.gpg file. So maybe HARPOCRATES is the passphrase of the file to decrypt or extract the the text.

![](attachment/f5712ed61587ee7de4e4fe4720fead3e.png)
logged in as jc and was able to get bob's pass.

![](attachment/004bb8c4fa50beb18e48884d028baba8.png)
we can see bob can run all the commands.

![](attachment/767ba70e431ec8372cfc2373cf8b87f1.png)
so did sudo /bin/bash to get a shell as root user. Thus. escalated privileges.

![](attachment/25b96788a7973110628695be3c8320cf.png)
Got the root flag.......................