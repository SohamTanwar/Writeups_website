**ip of the machine :- 10.10.142.135**

![](attachment/b91f805261565e1d8bb777fdf9bf710e.png)
machine is on!!!

![](attachment/0d326a6531142a8ff111540fecaac257.png)
found some open ports...

![](attachment/428fd6d50bca8c3ff531213132874f71.png)
when visited with ip address assigned found a windows web server.

![](attachment/c44ca57c5c3c74aeb596b02b497db539.png)
Some server related info from aggressive scan.

![](attachment/f439a89c30392fbad12babd1712ccbfb.png)
Info about SMB that is running on port 139.

Now will dig more towards smb and then will go for directory fuzzing.

![](attachment/caa6220c91b38e850fb79f98f9efbdbc.png)
found some shares, let's try to access any one.

![](attachment/d61f778e8acd3f821682c066feb25a4f.png)
was able to connect to one.

![](attachment/0a818013c60174b699de8fbf9717ccb1.png)
got a file.

![](attachment/1f6bf3dc1fe3f88abdc7bcb74ceb7229.png)
they look like base64 to me.

![](attachment/154e2e75ddcdc21261950687b2d6cce8.png)
was right!!! got two possible username and passwords.

directory fuzzing was not working on default server port 80, so went to do directory fuzzing on port 49663 which is also running the same web server. Didn;t find anything in the web servers. So now will be uploading reverse shell directly to the share because we can write to it to get reverse shell.

![](attachment/c5fe0bbc01c7824b46521fea58100212.png)
created a shell using msfvenom and with extension .aspx because of asp.net and we have to make the shell executable so that we can invoke it.

![](attachment/a537e88549857a58dca072879fd73c72.png)
added revshell.aspx.

![](attachment/faca26a72dcea4ff25cde5be6adefa70.png)
tried to invoke the shell with the help of web server but was unable to do it at port 80. But at port 49663, during directory fuzzing, it showed a much better response, although not a satisfying one but can we use it to invoke the shell.

![](attachment/b9f398e2634852d56d7fc77ec9a22a25.png)
oops!!! nothing happened!!! Did we get the revshell.....

![](attachment/7579d7edce05c4cd796bdfda1615e92b.png)
yay!!! got it.

![](attachment/bd6ceb5188da03f827d73dff6ff6f8de.png)
got the first flag in Desktop Directory of Bob. Now let's go for vertical priv esc.

**machine went off at this point so restarted it :- 10.10.72.27**

![](attachment/0cd5a3632bed90d67e8f9bed647ec0a3.png)
whoami /priv can be used to see privileges of the current user logged in as. SeImpersonatePrivilege looks interesting.

![](attachment/6d2731e4ccb5a96fdced0f526c6932b6.png)
found this on github.com to escalate privileges. Let's follow it step by step.

So after README.md, here's what i'll do, 
will take printspoofer.exe and nc.exe and upload it in smb share and then will use printspoofer.exe to invoke another reverse shell which will get us privileges.

![](attachment/f40d040c977449e300dd205169a73392.png)
uploaded Printspoofer.exe and nc.exe to gain a revshell with higher privileges.

![](attachment/4f2a8bf31124c624ebaaa1fa5cd72a69.png)
escalated privileges.

![](attachment/17b17cb22ee85749009a09144fcab07a.png)
got flag in desktop directory of the administrator.