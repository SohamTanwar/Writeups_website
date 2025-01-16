**ip of the machine :- 10.129.5.139**

![](attachment/047e06bd5b88020ad562012e26705b7d.png)
machine is on!!!

![](attachment/af3035bcd2c05f19465be6802ff8b261.png)
oh! a lot of open ports!!!

![](attachment/357edb7d94cfedabd64149c289d0490a.png)
Did an aggressive scan and found that a lot of http servers are running and let's try to open all of them one by one...

![](attachment/10f0f563701cba6b92753e9f3dfbdd26.png)
But only one at port got to see something as in rest it was all 401 status codes.

![](attachment/356b956ad37699a81a78b159709148d0.png)
Found here a version...

![](attachment/235e08d51ede55112656a9d66134f0e7.png)
found activeMQ version 5.15.5 on port 61616.

![](attachment/11f9903fd858a4565c95b5ada2706e8e.png)
After digging with some keywords found this exploit...

![](attachment/9b7e7e8ad7208eb04686f3ed39dd4483.png)
Let's try to run this exploit...

![](attachment/7c829560d7b5dfd9d64b64765831c5a9.png)
First, will be using msfvenom command to actually generate a reverse shell payload.

![](attachment/b40c197076690ab725b5fd3382a76d02.png)
Then starting a python server at port 8080.

![](attachment/c4abec4e16e513db5c3bf947da9bf443.png)
Then changing the poc-linux.xml file (changing ip and port). So this file will download the test.elf file created on the attacking machine and then execute it to give reverse shell and this is the deserialisation vulnerability in apache activeMQ which will gu=ive us RCE.

![](attachment/02e9a304a0d07292c026f6c3ce6ac010.png)
executed the exploit....

![](attachment/999b28fed174bc5713704ba410a952e8.png)
Got reverse shell...

![](attachment/bf0a70613439535737bf1d1b8332d8c3.png)
Got user flag....

![](attachment/9e366475a7a817700b9c352c353bc806.png)
did 'sudo -l' to see what commands current logged in user can this.....

![](attachment/e6ea212ea30d0abf71bb917d036cbdd3.png)
So found an exploit to actually exploit nginx which can be run as user... So basically according to this exploit a pwn.conf file in /tmp directory will be created where i can run a server on root directory as root user in the attacking machine...

![](attachment/6f52f46a2ee3233cf99cd3907082d71a.png)
So after running the exploit a pwn.conf file will be created.

![](attachment/dacd4f47d5dc293a347380ef651a52a4.png)
Will be using -c option/flag to set/enable to configuration created.

![](attachment/818adff0709f5905654da7b84621559c.png)
So in sockets found 1337 at localhost of the machine started.

![](attachment/57ce49306053573763f675bf08b2042f.png)
It showed root directory...

![](attachment/c9b340c5430d68938d7596f5021168dc.png)
So directory got the root flag...

But still there are some ways to escalate privileges which can be uploading a rev shell and then going on web interface to get the rev shell as root user.
![](attachment/089b7de9834ecb842383edeb82a136a4.png)
Can see root directory...

![](attachment/95d3803cba414dc22b0ac01a9c6e2781.png)
Can also look for .ssh in /root directory and then put you generated key in authorized file in .ssh. So that ssh as root user can become possible...

If we can access everything a root user is accessing so we can see /etc/shadow for the hash of root user and crack it for priv. esc...