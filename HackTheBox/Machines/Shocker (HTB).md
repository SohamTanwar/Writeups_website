**ip of the machine :- 10.129.6.237**

![](attachment/98bc7fc5be896292238f56bcfc3ec235.png)
machine is on!!!

![](attachment/b5f6ce4a324acbc3e819a13631acef5d.png)
Only two ports are open!!!

![](attachment/2756f3a22a2f5bb21a03abed56f640ce.png)
So port 80 is running http as usual and port 2222 is running ssh.

![](attachment/82c64bc5ee2e1b42d9906d325d277fa4.png)
Found some directories, All are 403 except one which is the default one "index.html". But still out of all "cgi-bin" seems different... Let's search something about it

![](attachment/a7005804c88a54ae0d31e4ed18c85ab1.png)
So i came across this exploit for cgi-bin...

![](attachment/08bb69d9b6b26a4d9e243d07d0343ca6.png)
So exploit-db exploit was not working even after fixing errors in the exploit, so searched for new exploit with the CVE and found one.

Again this exploit not working some how so learned about the CVE more and then it said that there should be a script whether .sh, .cgi or .ps1 in cgi-bin directory which can be then further exploited by adding payload through exploits to get the rev shell, so thought of doing directory fuzzing again in /cgi-bin/ to see whether we can find any script to exploit or not.

![](attachment/834f5215f650ac206606bb882ea7b0aa.png)
So used dirbuster for recursive directory fuzzing and found user.sh with 200 status code, let's see it...

![](attachment/a92d29e24001d86a4232008bf5e05e0f.png)
Just an uptime test script, now let's use exploit because now we know the correct path that it is not /cgi-bin/ but /cgi-bin/user.sh.

![](attachment/a00f4d5fdf3c25c21d8ad88ea2333f32.png)
So using a metasploit module for this and set options.

![](attachment/0d91effb263e48755231e09231c74628.png)
After setting options enter "exploit" and a meterpreter session will be opened.

![](attachment/0d09144877283ffe221db4bda756ad80.png)
Type shell and then above python script to get an actual shell instead of using meterpreter shell.

![](attachment/703d266f6a8fe787e9c2968408d4f322.png)
So went to /home diectory and found one user "shelly" over there and got our first flag.

![](attachment/5150bf6167aabfe07f26ab59eaf5d34b.png)
I just realized that i had shell as user "shelly" only, so did "sudo -l" and saw that user can run /usr/bin/perl as root user.

![](attachment/b8d4fbdc0e235ed69398bfe43b505dad.png)
So will be using this command from GTFObins in order to escalate privileges.

![](attachment/820342245fd1e9443d46758249951cfd.png)
Escalated privileges and got the last flag.