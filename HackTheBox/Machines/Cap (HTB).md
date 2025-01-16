**ip of the machine:- 10.10.10.245**

![](attachment/6996c7f3d84bb89073821f027ebcfd52.png)
machine is on!!!

![](attachment/9ac3fa35f14c410e2f1952b3ae024eba.png)
only three ports are open.

![](attachment/5750ba6d6faf838d00e19ab467824161.png)
a security dashboard is hosted on the web server.

![](attachment/9a7fd4e594179dcf20ab5b7e8a2660a7.png)
directory fuzzing showed a directory and rest seems like commands to me.

![](attachment/237ac965f8b1ec41a514f34eceb91110.png)
a security dashboard with only one interesting option "data" and one possible username "nathan".

![](attachment/3a33757e0d76083136d8fa5bfd047c37.png)
in security snapshot tab it is giving us pcap file for analysis purpose let's try downloading it and analyse it.

![](attachment/9db651d04fa41001e3ecf04e4e7ab8b4.png)
Found nearly nothing!!!

But in url it was written like /data/10 where 10.pcap is the file we downloaded so let's start changing it and see whether we can get some more pcap files to analyse or not.

![](attachment/ff09397197be9ce4fcf3578a39df4bf9.png)
on writing 4 we got a file named 4.pcap

![](attachment/d03241c197610eaea3c281f5b4efa38c.png)
Found nothing interesting..... Just normal HTTP traffic.

What if we change 4 to either -1,0 or 1 maybe it can give a file containing something interesting. This type of vulnerability is known as IDOR (Indirect Object Reference).
![](attachment/326c07ccdcd8221d5c1830f0ea27d8fa.png)
we can download on 0....

![](attachment/fbf7908a759abe58ec8668bc0775a846.png)
Now in the pcap file found some FTP traffic and followed the stream and found some creds.

![](attachment/953be305363e758f470df9db8ea4ffe8.png)
was able to login with creds. and found some files. Let's get them and analyse them.

![](attachment/bf726eb57c2c1d9d1f5d2374ad013550.png)
got user flag..

![](attachment/16afa3fd1c8de42bc152fb177c6244d1.png)
it seems like a root shell to escalated privileges.

![](attachment/b600812bd5427699f2632905652196a8.png)
i used password spraying (same creds. being used at multiple platforms or accessing of sources) as nathan used same creds. for ssh as well.

![](attachment/b51b1d8a8b4774790b5f8b13646aa059.png)
There was no point of running linpeas and analyzing the attack surface for more ways to escalate privileges as a script is already present so just ran it and thus did vertical privilege escalation.

![](attachment/dd2dbd293f377b1eabb249d80bdf70cf.png)
got root flag.................