**ip of the machine :- 10.129.2.249**

![](attachment/77bc305449ae3dac6b78cf9f44482d84.png)
machine is on!!!

![](attachment/73cc7db313b40426b1a8550bc9d386f9.png)
Found some open ports out of which a lot are unknown so let's see what we can find about it in the aggressive scan.

![](attachment/3c28da336a5474815693cabe13441185.png)
So got versions, and started looking for any available exploits but didn't find any for ssh and http server...

![](attachment/221cb40a8e38b1493045dd1c70f9d149.png)
Went to the website and it gave a hint "IRC". Now what the hell does that mean??

![](attachment/376c34df5e695a8d0ff4addb70b1ef81.png)
So IRC is a protocol used in 1988 for real time messaging. Wait is it really running on any port!!!

![](attachment/995b17b216436d0f688d3cf11560fc2f.png)
So some ports are running IRC protocol.... Let's find some possible exploits for IRC protocol.

![](attachment/83ec4aa8eea60b6e3ad74f8f95332133.png)
So did another nmap scan for all the ports and found unrealIRCd as the open source one running the IRC server.

![](attachment/c216d75bfc6fafb0890d7896e99d34b4.png)
Don't know about the version of UNrealIRC so have to brute force / hit and trial with this exploit as it was the first when i wrote exploits for UnrealIRC.

![](attachment/b83e3df60d4c1a83f7cb00593711f22f.png)
So basically exploit had some reverse shell payload so -payload python means used reverse shell payload of python to get reverse shell.

![](attachment/2731dbd703c670d8d062654f65f8d1c5.png)
Got one as a user...

![](attachment/f7c6ebeeeea9f7ff1a99d2ffd9478672.png)
Got another user in home directory...

![](attachment/6c4c40aa33904eb38ab584aae11d8f31.png)
Found user.txt in user's home directory but cannot view it...

![](attachment/9dfdb1a1add8017c6e58cd17fd6b47bc.png)
In user djmardov's home directory found a .backup file...

![](attachment/995bddc3ca419ffbddf4e1e0a31a1f6f.png)
Does "steg" means steganography and we have actually got the password of an image containing something hidden.

![](attachment/f07eb48a0e678629184a8aa769c2a650.png)
Let's download this image as it is the only image i've found.

![](attachment/3543cb2d705d7666d51d8fe64d7acc68.png)
Was write got a file by the name pass.txt.

![](attachment/f53d7cc83c7f85637eda84c912e338e1.png)
Let's use it to login as another user....

![](attachment/4da51135ba681fe74eadf2eb262ffe3a.png)
Finally logged in as another user...

![](attachment/fa57fa4c162af251c23670bdc0bbaff7.png)
sudo command not found!!!

![](attachment/ff86cd717b452318fc4a26864ca5c4b4.png)
Looked for SUID files and found one strange one by the name "/usr/bin/viewuser".

![](attachment/5b0b0f9591c1cfbd7de32a7935f50d49.png)
Ran the file and it said a specific file in /tmp directory not found...

![](attachment/67f3a16cdc2eaed866f7bb2fee3d8158.png)
it is an executable/binary, that i know.

So here's an approach for priv esc.
Now i will create a file with the name listusers in /tmp directory which will contain a shell.

![](attachment/f8041a959c1adec5e2c41d39c4e57a41.png)
So first created a file and entered a shell in it and gave executable permissions, so when /usr/bin/listusers got executed, it also executes the /tmp/listusers file which contains a shell and it ran as root maybe that's why it gave a shell as root user.

![](attachment/3572961b5a6db1389b77620c039a53a8.png)
Got the last/root flag...