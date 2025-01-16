**machine ip :-> 10.10.223.107**

![](attachment/7d2f95f3ed420f69f957a2a419c04da5.png)
machine is on!!!!

![](attachment/8e32cef74f8f928e2c43efe5008eb94a.png)
Did an nmap scan and found some results. According to the versioning scans i am assuming that it is running a windows server and SMB but also has a web server running.

NOTE:- Didn't find anything pleasing in the dir scan of gobuster.

![](attachment/84df4eca2e861d75d279e033cd33c272.png)
Found this js code in code snippet. It seems like the website is fetching some information from an unrecognized port which didn't come in port scanning and let's see it manually.

![](attachment/059e971dbb79405376245066402c9686.png)
Apache Tika server is running. Let's see if we can find some exploits or not.

Didn't find anything pleasing on exploit-db but found a module in metasploit.
![](attachment/048e43f08dc5e49b739742444479e366.png)

![](attachment/6936c115ea3f33a9c61a2899d53edeb7.png)
set all the options and we will get a meterpreter session.

![](attachment/34706ca41340894ee038e52a5ba4e98d.png)
so first did "getuid" which is just like "id" command in linux to see username we are logged in as. Then got a file named user.txt so viewed the contents and got the first flag.

![](attachment/b4d66699204fc47632c1c20b97580b7b.png)
now background the session using "background" command and will be using a module named "exploit suggester" which will suggest the exploit we can use on the target machine depending upon the background session of meterpreter.

![](attachment/91ae3c1f0531242dc472e63468d25f4a.png)

![](attachment/ee7f7786319cd6d892e91aabe149184e.png)
so this module suggested some solutions depending upon our target machine. Will be using first one which can be used to become admin.

![](attachment/993134e6179a63ebf214c19dd8fd3c48.png)
became admin now just need the last flag.

![](attachment/b71ba4d50abe4ac4f0a21bc3bcb98c8f.png)
found admin flag in Desktop folder/Directory of Administrator.