**ip of the machine :- 192.168.122.101**

![](attachment/ff56768a7d98a2784da1a6cda1cee898.png)
machine is on!!!

![](attachment/73d0780eb95f238ad59f6c2c1ba22bd6.png)
Only two open ports!!!

![](attachment/8fe6ef6119b9fe77e12fd890f3217198.png)
Performed an aggressive scan and found one disallowed entry in robots.txt.

![](attachment/c574c210b4a1a534fd3587e0fcf914c8.png)
Nothing on the web page. Let's check the src. code.

![](attachment/a3de9091cfa083258f59244c2dea14c1.png)
Nothing at all.

![](attachment/b1950ecf2bd3dc45cafc8feea9eaabec.png)
Nothing interesting in robots.txt as well.

![](attachment/04cfd341f7615e15a42328b2de790ce9.png)
Found nothing in web directory fuzzing as well.

![](attachment/545bd7f5a3412983d9d33ff3234f7cc6.png)
Found nothing by feroxbuster as well.

![](attachment/aab296298fe74070786b6a435c9ddcef.png)
So, went to one of the blogs by hacktricks and learned that /console directory is sometimes accessible when we want to debug the web application in wsgiserver.

![](attachment/89b00257dfec47d7c859fc7838dacf25.png)
It showed an error of django and saw one hidden directory which was not displayed earlier anywhere.

![](attachment/2e0e6fa7a4bde5fde22092ea256c1588.png)
So, visited the directory and found this web page.

![](attachment/a49719c4b2664b11a09515a015555928.png)
Found this and nothing interesting.

![](attachment/97ed2988a300184cef651c26dc8cdeae.png)
Also found a todo list. So now it is confirmed that django is being used at back end in the web application.

![](attachment/773d580264c56bee9985b2792b2f8854.png)
Got a bunch of errors after visiting this web page and got the version of django running but found only one thing SQL injection.

![](attachment/4ea36cf4ec00f47ebe285827731b94a1.png)
So, saw some errors and i think sql injection is possible on this web application but where, let's find. I also searched that this version of django is actually vulnerable to SQL injection, so let's try.

![](attachment/c3121ff3ec2bf400712a96dcc49b92cf.png)
So, at this web page it was 1, so what if i do it 0.

![](attachment/c3b6b44c957abc14bc8616b1460707a0.png)
If it was a web page, it should have shown error but nah!!! So, let's try the most basic SQL payload here.

![](attachment/a842e4b1d6ba5676abea9df44d9c5eeb.png)
Oh!!! It worked.

![](attachment/296227ab7e204647c6761a28adcb8f2a.png)
So, got tables names for information_schema.

![](attachment/c4042f69f884c79c2091eb5e6d40d0c5.png)
So, from users table, got a possible username.

![](attachment/0b712e96c7eedf6d98345962808f7022.png)
Also got passwords.

![](attachment/c45fce5c5eaa441f4c3aed5467e68a5e.png)
So, logged in as webmaster user.

![](attachment/05bad71e22de37021f353c7df48540b1.png)
Got user flag.

![](attachment/924d17808e902b45ae122614380089f2.png)
So, there was a directory in user webmaster's home directory, so went to the directory and found a notes.txt with some creds. in it which are base64 encoded.

![](attachment/0b184769bf68f22c73e1471edf5af07f.png)
So, got it. So 'linuxmaster' user was not showing when we did sql injection so let's login as 'linuxmaster'.

![](attachment/b32d0c5b183ccdd9985e740fdf54a0ad.png)
Logged in.....

![](attachment/267fb994450915759f883fae728c1bf8.png)
Found nothing in linuxmaster's home directory.

![](attachment/8961faebe62ba93949665ee4cbcd11c8.png)
So, user linuxmaster can run a bash script as root user but what is SETENV???

![](attachment/a53ef09dcda9c2e9a1fe0fd0aee97854.png)
So, searched for it, maybe it means that when executing a command or something we can set our own environment variables and values assign to it. Let's see the script then.

![](attachment/4c8f1748a474f76915862b081ce32519.png)
So, the script is calling tail but full path is not specified. But when called the script it is showing only last 10 lines of the file, so we cannot use priv. esc. method of less. But path injection seems possible.

![](attachment/157a298bf50ff9996697e37be37cf0a1.png)
So, tried creating a symlink of tail with /usr/bin/bash such that when the script is ran as root user we can get a bash shell but it didn't work.

![](attachment/5e921951456d8c381f5fd1a0afdd5aa1.png)
So, user linuxmaster can also run vim, so trying with vim now.

![](attachment/55508a2f2ec67d672bd9a4223cb7f51a.png)
We got a new file in vim. It means that it worked.

![](attachment/92cdaede73b0e0585b94857e6fa9c5bc.png)
So, let's try this payload now.

![](attachment/de60f24c402ad7aaf16ca6246bad2840.png)
Got root as well as the root flag.