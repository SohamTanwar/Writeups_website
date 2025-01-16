**ip of the machine :- 10.10.228.203**

![](attachment/b7151a1a5914b51221732e5249dfc27d.png)
machine is on!!!

![](attachment/60bb521f82ba8e1d4b659e30ef3bbaef.png)
ftp, ssh and smb is running on default ports...

![](attachment/6531db8792842d6bacb191374f190e9f.png)
ftp anonymous login is allowed...

![](attachment/86f30934b311299004b6219df00bcd34.png)
anonymous login successful...

![](attachment/2fec7e6d9caabbc0aaf725b647c9343e.png)
found a directory with some files, let's get them...

![](attachment/52fd1fe166699aa1d3e981187b194a5c.png)
So used nmap smb-enum-shares script to get all the shares on the server.

![](attachment/221a1772013c17a1854d87aedcada040.png)
logged into pics shares and found some pictures, let's get them...

![](attachment/7fb30ce188d1244eb4bec878c1040a3e.png)
I think so clean.sh script is designed to delete every thing in the /tmp directory.

![](attachment/70be9c7ef04addf25a54adc5e59dfbf6.png)
nothing to delete means no current files in /tmp.

![](attachment/182bd8a327347cf1498f4fd0a0193fdd.png)
well!!! have already exploited anonymous login.

No file is of use. Except that we have anonymous login to ftp. Let's add a revshell over there and see what we can do....

![](attachment/4f2e6744aea4a0726290b295093c87e6.png)
So added revshell in clean.sh file and then uploaded it on ftp server directory where it got updated and as other we have read, write and execute all three permissions.

So start a nc listener on any port and wait a while to receive a connection as clean.sh is probably a cron job.
![](attachment/6d5caa019d28f1433648265666b8786f.png)
So got a reverse shell connection..... as username "namelessone".

![](attachment/e403d3a5540a492d1c155466666a8e83.png)
got first flag...

![](attachment/0bb1cd8721193cb58c3ed9430833c3a1.png)
there is only one user and didn't find any interesting files and directories. Let's do "sudo -l" to see what privileges does this user has.

Sudo -l is asking for a password which we don't have and didn't find any as such. Let's check for SUID files now.

![](attachment/2faaf8bbaae8b22c2197028e54637301.png)
got some binaries, let's go to GTFObins.

![](attachment/299333b77551e80d485178572350ce62.png)
Saw on GTFObins and found that env command can be used to escalate privileges. Basically /bin/sh was in env variables, so called /bin/sh in /usr/bin/env in privileged mode to get root/pwned shell.

![](attachment/9e0c5a663d520cbdcb6361bb1a0fcd88.png)
got final root flag.....