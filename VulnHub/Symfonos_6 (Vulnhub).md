**ip of the machine :- 192.168.122.35**

![](attachment/4a76932e51ee337af032c0336a11ee32.png)
machine is on!!!

![](attachment/31894a4eebf86746d4dc70bb4da5eefb.png)
got some open ports!!!

![](attachment/603f24614aa02330505ddea99aee87d0.png)
did a versioning scan.
![](attachment/c21804046d9fd4600ef7e7bacba01eb4.png)

![](attachment/206aa23a1e53d115c643da73fa3de8eb.png)
Also ran gobuster and got two directories to look for.

![](attachment/f3e064ec57ad987f159e5eb070b0af4f.png)
at port 3000 another web server was running so went to check that and found this webpage.

![](attachment/af0cc8389432c57590e7d8d25eeaa910.png)
found two possible usernames.

![](attachment/767d02f0b88293f16312f7e1d34fa129.png)
at /flyspray/ found this and when we click at login there is also a login page and register page as well. Let's register as a user and try to check for XSS.

![](attachment/fe9f55e9f4af1aed1d5efdc2d3d63960.png)
on searchsploit it seems that xss is a very common vulnerability.

![](attachment/5440f8ef6d91ddfe1ce563ae4e7b56d9.png)
on register page tried to add this.

![](attachment/19fd31a9580109eb28b5182c617444ee.png)
After logging in, going on "edit my details" tab found an xss thus confirming xss vulnerability.

![](attachment/67478d0b8fc4099579ec0121b4fa31a3.png)
as we know xss vulnerability exists so we change our real name to the exploit from our machine. There is xss vulnerability so it will take it and execute it.

![](attachment/1cf382e8ffdee1b77c1cd77bdb419480.png)
In bug report added a dummy comment.

![](attachment/98a04bc3dce525aea2b8ba2c8b281d2e.png)
and after some time it got the exploit from our python server because of xss.

![](attachment/a646ba1339522d2fa9b2ad87edafcd82.png)
this was the exploit and it also stated that after the exploit is executed it will create a account with creds. "hacker:12345678"

![](attachment/bc9b06acf794a794bc013a3eccfc6314.png)
found creds. of one of the users after login

On port 3000 found a login page so let's try to enter these creds. there.
![](attachment/281362617eb97dce8a8f2803e789b3c5.png)
was able to login as the user with creds.

![](attachment/f8433012e61b2c666d259cd69bc429ba.png)
in one of the repo found this which means at port 5000 a REST api is running. But didn't find anything useful in the repositories.

![](attachment/c3bdf99694b5fe28a09c3708f99b5f8a.png)
but found the name and version of the software being used.

![](attachment/69693d0ec80560ee014f4a751046a49e.png)
found only 4 exploits but will use the first one.

![](attachment/f263a6821124e46bc95efb6eee195e57.png)
After running we get this. To fix it go to settings of the repo then git hooks and then pre recieve and add bash shell there.

![](attachment/9cfe330768a844b5ae72ec466d00a2ae.png)
add the reverse shell payload.

![](attachment/36121c7323dfc239ed777cf3a1d8a51a.png)
Now in index.php file in that repo add a commit to start the reverse shell.

![](attachment/96a5df4e1f8c5f75d6bcce097e390c32.png)
got a reverse shell through git.

![](attachment/57c7ed95b96874f54b11dcb797adbccb.png)
got possible users. Again "achilles". Let's try to login as achilles with same password.

![](attachment/fe9497f092b2f2871d3f836d27c451f2.png)
was able to login as achilles.

![](attachment/15c3287c9c010017c572579fcd10d37c.png)
user can only run go command.

So if we write the code in go to get a root shell or simply a shell with SUID permissions, we will get root.
![](attachment/3daa302ae5abf405aeb22eccb05ca439.png)
This is the script to gain a shell. In this, giving a shell SUID permissions in /tmp directory which will be run as root afterwards in interactive and privileged mode (-ip).

![](attachment/85537b8f9609522551c77d99ece62a54.png)
After running the script on target machine, will get a shell in /tmp directory and then execute it in interactive and privileged mode and after getting root flag is yours. 