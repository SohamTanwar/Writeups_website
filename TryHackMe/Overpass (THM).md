**ip of the machine :- 10.10.201.195**

![](attachment/dce11bd0a08baf7ae6b55c81e2eb5db2.png)
machine is on!!!

![](attachment/658d3762824ee45e83554958ed372146.png)
got some filtered ports, maybe because of some kind of firewall on those ports.

![](attachment/892a5a9e4d6824f461da76b08639d7eb.png)
So interesting ports are 22 and 80 only.

![](attachment/6d8efee372c4e578fdc0ec9552593501.png)
So let's go for directory fuzzing right now and then manual web enumeration.

![](attachment/9c08678a0ff5759661ee178952ca35b6.png)
got some directories.

![](attachment/34b08d792f1ce1778b2903b5264a8569.png)
in /aboutus web page got some possible usernames.

![](attachment/27bf0b3e5f17ac5aba746c370e4b4cd6.png)
found administrator login page. So on this web page SQL injection didn't work and XSS didn't work.

![](attachment/a83c6e1864c36e9ee9b63d8ca23b53af.png)
in view page source found three scripts.

![](attachment/373acec03e17ac51a354f79dc4352e80.png)
found the code. After entering some creds. they are validated at backend and when the response is sent like "Incorrect Credentials" then it will not login us in, but if credentials are right it will. So we have to manipulate the response.

![](attachment/4c68c321c34ad024a6373b1957c6f78b.png)
So added a Session Token to bypass the login page. So it basically worked because, in src code it is saying that if we add wrong creds. it will say wrong pass and then we won't be able to login but what if we don't supply any and just set the Session Token to be statusOrCookie which will be assigned after logging in.

![](attachment/6d0e7c26260b4cf54497314bdb683e6c.png)
got a private ssh key of the user named "james".

![](attachment/df1416e0af2e4ad694d4f2d2bd0a599d.png)
it is asking for the passphrase. Let's find it using john.

![](attachment/e7fda22218e3b2dad3d5c0e2fcd1336a.png)
found the passphrase.

![](attachment/8c46d77bfb8b87675ef2ccd968b6a646.png)
logged in as james...

![](attachment/3e6a43677ce51104f9c24713b629dca2.png)
found the first flag as well as a todo list.

![](attachment/b5416eb263b397ca55c4bed32b23927f.png)
"cat todo.txt"

![](attachment/cbde7d2a669bf716c7e4746b2c0f8c26.png)
in /etc/crontab saw that a script is being downloaded and executed.

![](attachment/f32a22edf72fdf77405af049c82c1061.png)
We can write to /etc/hosts file... So will start a web server on my system and create a file buildscript.sh and then it will contain another reverse shell and when it will be executed by root, it will get us root/pwned shell.

![](attachment/44f108ff061065cd6dfd7c3ba4dc33c5.png)
added revshell.

![](attachment/b39e1b23ac41a0f6b7aeb3b17182fcf5.png)
It will take some time to fetch the revshell but still it's fine.

![](attachment/eeaafec96df20f1792e8313ef033e2f5.png)
got root/pwned shell.

![](attachment/a7f307111f83953470aca0ed9beee75d.png)
got last flag...