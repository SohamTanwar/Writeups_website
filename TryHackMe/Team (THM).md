**ip of the machine :- 10.10.76.180**

![](attachment/f06da5185a29154154522c51f74cbe7e.png)
machine is on!!!

![](attachment/670e92fb3f6e81183c62ac55bab794ed.png)
got some open ports!!! will do aggressive scanning now....

![](attachment/50f4bd4a91c06136c0b3d76f7d1b90a9.png)
Found versions of all the services running on required ports.

![](attachment/18708e747a04979d1917f75adf4e8f19.png)
unable to login through default credentials anonymous:anonymous.

![](attachment/d8a5432e81381c33fa994fe7a64e6a5b.png)
A web interface??? let's further enumerate..... src. code.

Didn't find anything in the src. code so now will be using ffuf for directory fuzzing.

![](attachment/e1e670e77dac3469284efe38021b51f2.png)
oops!!! Didn't find anything...

Didn't find anything so looked at the src code again and found this.
![](attachment/20a28a4d9d51741a598d3b6c6bc64f79.png)
let's add it in our /etc/hosts file.

![](attachment/52f72f085f66dcfb4d4d70c26354a96f.png)After adding team.thm, it opened this site...

Now didn't find anything in the src. code as it is a template so will be doing subdomain enumeration now... using ffuf again....

![](attachment/7ca9a108e9ed60793fa8bb9e401b5124.png)
Didn't find any subdomains.... so used gobuster with different wordlist.

![](attachment/672b805954815b83d80e05554380bde4.png)
found some interesting ones.... So added the domain in /etc/hosts file and went to the domain.

![](attachment/2ff2a3d23b654229156902a9e18ce678.png)
found a link... Let's move further...

![](attachment/966d24cbc7dca6f0cda7dd9018e43cb8.png)
Just a normal web page but url seemed fishy to me like the query page is referring/displaying a web page which is present on the server so maybe we can detect LFI (local file inclusion) here, which is seeing any sensitive file present on the server and see if we can execute some commands to get reverse shell or not.

![](attachment/35703c9c39491fc2100b593e421cd212.png)
Confirmed it is LFI....

![](attachment/35355a21e020523eaa73e78e9163b525.png)
Now after a bit formatting found two possible usernames Dale and gyles.

Was unable to find anything to get reverse  shell then came to know that i didn't do directory fuzzing further after adding domain in /etc/hosts file on the domain, so will do that now.

![](attachment/b146f9e2e3bf8eaa67aa246c1917f0b1.png)
Found a lot of directories that i missed.

![](attachment/88c550e8f5cd56bed28e8be3363d5164.png)
We found dale username before while performing Test for LFI, so maybe we have to login as dale first...

Only robots.txt worked for many and not anything else.
So thought of looking for private key of dale but didn't find it in home directory so went looking for /etc/ssh/sshd_config which was displayed because by default an ssh key can be in user's home directory which it was not displaying, so went looking for above file.
![](attachment/d4332b095ded496cc160aa9c95053bbd.png)
private key of dale...

![](attachment/7b46642d50fe53403c4b43eb6dc17a59.png)
was able to logged in as user "dale" with the private key.

![](attachment/9ee72bafcb6e2de4e435f95270313eeb.png)
got first flag...

![](attachment/6c3a2d05c649b3e32f7c099bb78ccd3c.png)
So went to see for .bash_history file and saw this...

![](attachment/fcbece06b3f73e9db723a9e5a0d86247.png)
can run /home/gyles/admin_checks as user gyles....

![](attachment/318fbe2c550ddb4b0a9d77cefcffcdbd.png)
backup creation file probably...

![](attachment/7824cc34d53b36ebe7391a275cc5e776.png)
So don't have any permissions to edit that file so went to home directory to see more users...

![](attachment/81e190535c25624283672c271a457801.png)
wooh!!! we have already done that......

![](attachment/198a09becbe4505c478e8fc1abd5ed6d.png)
So after running the file as the user "gyles", went to /var/stats directory and saw logs, nothing impressive.

![](attachment/ca1212f644730d1b1f9f353a07af063d.png)
So after finding no clue, simply ran linpeas.....

Didn't find anything so went to /var/www/ directory to find some more stuff..
![](attachment/90b6fbcc0f4fb61945fb32435c5eb2c8.png)

![](attachment/cd452282e2403d3f2c760bd4f29f156b.png)
So found two scripts ,out of which one has a password of ftpuser.

![](attachment/b1cf287b04e233be2a3f8008ac9c6ad7.png)
So while running the script as dale, tried to do some random hit and trial stuff..... added /bin/bash in input...

![](attachment/8e9325c9415d0842d41c32002d64564d.png)
and got a shell as user "gyles".

![](attachment/0e5bca9eaea87c3d81ff98ceb44afb6f.png)
![](attachment/7b6d807fee7fc6b39e55dc914e1f21d7.png)
So got two interesting files for .bash_history file of user gyles.

![](attachment/e4015331da25d8a43dc39046c474e8c7.png)
as cron job in /opt huh!!!

![](attachment/688082e22c78549589f2a83fe70c514e.png)
So in backup directories multiple files are there that can be edited by people of admin group which gyles is a part of let's edit one of them.

![](attachment/515cf83813097d40e7a50dfa83261d13.png)
So added a reverse shell in one of the two files.

![](attachment/9cda720897cbb587065ee8b750cf8bd2.png)
So after adding reverse shell we have to wait for like a minute as there is a cronjob running and then we will get root shell.

![](attachment/2542163ef88e0f89e0f7fa17490caafc.png)
Got root flag.....