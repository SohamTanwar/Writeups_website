**ip of the machine :- 10.10.200.53**

![](attachment/cd8fa74c0d2fef77f66586c5719e7f8f.png)
machine is on!!!

![](attachment/d306871c8ba2e5549a7d4763b4c45c7e.png)
found some open ports!!!

![](attachment/815f9419583b7b9cd9db2d739f0b2881.png)
did aggressive scanning!!!

![](attachment/d0f8a42f00d16acf50be26f89827e1a5.png)
did directory fuzzing and didn't get some satisfied response so though of using another list and got some convincing response there.
![](attachment/f55451df9b9dcfbae1b86749dcd6f4b7.png)
what is spip?
![](attachment/00f05d90b9abceb556c6bebe1f373248.png)

![](attachment/ff5c00eae895aecb929f0accc5f6dec5.png)
Found spip version in the source code, let's find any possible exploits.

![](attachment/6c39a0c0129dbd2a44e7f14b30827053.png)
Got the exploit.

![](attachment/960d5a65b7c8ba303b6dd853b0a9605a.png)
was unable to get revshell manually so had to convert to base64 and then decode it later on and further piping to bash to get a revshell.

![](attachment/247040eeac7960eb2cff2faafe31bc98.png)
got reverse shell....

![](attachment/46c92fa962d3147c59ba4a5c47e60b7c.png)
one possible user "think" and user.txt found....

![](attachment/220a1cfe1685b2e83ed44e8066cf8717.png)
was not able to find the way to login as the user "think", then saw a .ssh directory and took the private key and logged in through ssh.

![](attachment/d75e0c06608c5a125657b15666aedefc.png)

![](attachment/91dd7a17d2a0b48fc827705488008f32.png)
oooh!!! what shell is it I wonder!!!

![](attachment/846c6b9ceaa6524992dd471cff6b03d7.png)
was unable to find anything useful about the ash. So saw hint and then went to see app armor configs.

![](attachment/9a4ee7972da420c4852a212ff798b680.png)
found /usr/sbin/ash in apparmor.d directory.

![](attachment/8df91bb0ac28974bb4b1478814ba4f1a.png)
/opt/ directory access has been denied in this shell. Let's see if can shift to bash or have permission to shift to.

![](attachment/d68d9f9b57c68b128e87c79d71c5c2fd.png)
can execute bash shell. So let's do it.

![](attachment/77d59366cfc06bdb003413fe7c552c0a.png)
found some files and most interestingly a script. Let's look at the script.

![](attachment/c228464e87bb04deca2407b806b98965.png)
i typed "vim run_container.sh" and not can change in the src code.

![](attachment/f35c8e7e2f3a7adcaa5469c64d94353a.png)
was unable to get the pwned shell, so did a search for suid binaries/files, so found run_container is sbin as well.

![](attachment/ebcdd3bce11e4ea60f62fbfd423afc07.png)
so instead of creating a copy in /tmp directory, directly added the payload and executed the /usr/sbin/run_container binary and then got a pwned shell as root. Now to get the root flag got to the root directory.....