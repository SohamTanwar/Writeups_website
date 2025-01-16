**ip address of the machine :- 192.168.122.232**

![](attachment/26c793814a312b347ce6ecca85e5b0d2.png)
machine is on!!!!!

![](attachment/36f4dd9bce432dd8e0435b986ad6818b.png)
will be performing versioning now.

![](attachment/1c69e9684a9caa07e54108b87dcce0d7.png)
Found version of the services currently running on the ports.

![](attachment/d54a48949101198968ef260ac0ebf8c1.png)
inspected the web page and found something in comments of the source code ("underworld")

![](attachment/18df6c33b48514a3dbb55293aabd0cd0.png)
oops!! found a directory, let's visit it and see what we can find further.

![](attachment/00fdbafce23f12b8c1834b554e28bdca.png)
using dirbuster found a web page /cgi-bin/underworld/

![](attachment/7c281f75c8efe91e72be57a262ae7402.png)
showing uptime on a web page.

![](attachment/3e8f3b54e11302ca0a4bac2daf7ab3ca.png)
found this that cgi-bin is a folder where executables are stored and maybe underworld web page is an executable showing "uptime" 
command.

with some searches found out that it is a "shellshock" vulnerability which allows attacker to execute a script remotely via bash shell.

![](attachment/14aac2cbbb7b3e9ad2cfc4f810369af6.png)
got an exploit in metasploit.

![](attachment/4fe0a3e328d2e664690761509e915779.png)
got a shell and created a meterpreter session.

![](attachment/49354c262e3e114e7aaa5936718809f0.png)
while finding things manually found out that there are two users which means we have to go for horizontal privilege escalation first.

![](attachment/7b0e7185c1092ddfa07272574148deb4.png)
also found that in /opt directory there is an ftpclient directory which means that an ftpclient is running so let's capture that traffic on local interface.

![](attachment/aa0f15c2ea4382afb684e2fdae5800bd.png)
capturing traffic on local interface to see if a user login into the ftp server as ftp server is not secure to access so maybe we are able to capture something useful.

![](attachment/40c4898b94e54f44b6a55634eb19c75b.png)
we got something ftp data and it is not encrypted.

![](attachment/badb3662678de718aa37c890880b5b32.png)
Aye!!! got it something juicy!!!

![](attachment/07a1a98fe1959d82902764b893e95ed7.png)
logged in as "hades"...

![](attachment/fc6a3802b96bace602da9c659029182c.png)
after logged in as hades got to see the ftpclient directory and saw a python file.

![](attachment/2d2a76b1852b835aecf5ea6aa2d32609.png)
the file ftpclient.py file is owned by the user root so if find a way of adding the reverse shell in that file we can actually get a root shell. But it's not writeable.

![](attachment/563b8290b2cb03a9f41a76cf9c137a5a.png)
ran pspy script to see all the background processes and the script is running.

in source code of ftpclient.py file, a module is being imported and all the libraries are stored in /lib directory so let's see can we find that module or not.

![](attachment/d9ebd6175939d25a5fc9e91d5972eb6f.png)
got the module and writeable by gods group.

![](attachment/7d99f3829071fb4fa3bc6ee531340925.png)
hades is in gods group only so let's add our reverse shell there.

![](attachment/2f8c7e6f4de6a6f9b86a1092a71b7360.png)
add this in ftplib.py and wait for reverse shell at port 1234.

![](attachment/ec5d8c17382c039afbb757ff2161f9f2.png)
got root shell.

![](attachment/1f184a3ba62ff5f146c9f9b7f5eb822d.png)
got it...............