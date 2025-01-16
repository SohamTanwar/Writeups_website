**ip of the machine :- 10.10.46.107**

![](attachment/67e8213d9c267184850f1cae204968eb.png)
machine is on!!!

![](attachment/9a91b071bf46ab50c9b317f7558cc1ca.png)
Got two open ports!!!

![](attachment/02f59ce6039654a5d11a6560340b94cd.png)
Found version of the services running and also one disallowed entry in robots.txt.

![](attachment/6abdac117cccfbb7882eb71d0de40982.png)
Just a normal website with no clickable links.

![](attachment/33074dc79f1a180f1466a0e05008e04c.png)
Rockyou!!! Hmm interesting!!!

![](attachment/983443e5b0a136df6e6fa70c1be43f09.png)
Found a possible username "meliodas".

![](attachment/a130ce75386b0aa7c9a5b2ae43876565.png)
So, after getting a username, rockyou hint and only one service to brute force. Ran hydra and got the password for the user.

![](attachment/529097eab5bd374c90ef1d829e38cf19.png)
Logged in through ssh and got user flag. Also got a python file.

![](attachment/b9339a11ddb4b866a2f51c9eb8e5d52e.png)
So, we can run the python file as root.

![](attachment/7ea702f738e80aba346d4b5c90556137.png)
we also have permissions to edit the file.

![](attachment/2626c87dd092f813964547588868ace9.png)
Added the shell payload in bak.py file and ran the file as root user and got the root access.

![](attachment/36bc78d2c872e9c938db83458dbcd04b.png)
Got root flag...