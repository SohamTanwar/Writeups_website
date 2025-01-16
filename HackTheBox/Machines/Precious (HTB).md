**ip of the machine :- 10.129.228.98**

![](attachment/e2791a32782c2d9be984c31d83850840.png)
machine is on!!!

![](attachment/f6c7d61e3d71baa29388c07f5b4b7553.png)
Only two ports are open!!!

![](attachment/8a5ff17403cca4a7f1eab22bbc19d9a7.png)
It seems we have to add precious.htb in our /etc/hosts file.

![](attachment/05a8a002c2b28839977f59fbf409d437.png)
oops!!! let's see what is it...

So directories and sub-domains found in ffuf scan...

![](attachment/38228085c23d89aa6e4cad5629ea469b.png)
So didn't know much what web page to pdf was doing, so did a more verbose scan for port http, and found another software running with nginx.

So tried to analyse the site in burp suite and saw the runtime..... in response headers indicating that the applications backend is probably running in ruby.
![](attachment/d7b837423acd7d1f2a35faa6163242cd.png)

![](attachment/635fc7295194ebc55e77fc089e22fac4.png)
Some kind of url filtering which need to be bypassed.

![](attachment/42c65efe167cd7d8dbda1c0717c2092e.png)
So "%20" means "+" which is replaced by space and then it is reloaded after 5 seconds so this means this payload is actually working and by the way using back ticks so that can write payload with spaces inside.
![](attachment/a4dccec24ddc0f76d48826be7f8e6fd4.png)

Let's try to add a reverse shell...
![](attachment/dad41d08291bf1e36cca3cba1bf38178.png)
So instead of sleep in back ticks add this reverse shell payload so ruby compiler will execute it and you will get reverse shell.

![](attachment/44ab124bd5e7ef2a03fb0f4053fd89a8.png)
Ta-Da got it!!!

![](attachment/0e299ee5ba4530bca01aaf3dd12fd3a8.png)
So found creds. of another user "henry" in .bundle folder of user "ruby".

![](attachment/e123bcefbd718b2013189fbf8bc28a45.png)
Got our first flag.....

![](attachment/831e9e713cb6457b385bb49005e1e826.png)
So user "henry" can run a script in /opt directory as root user...

Let's view the script.

![](attachment/d50896fc2affde5b649397b8a983c811.png)
Well didn't understand much, but i think so it is comparing the dependencies in these script to dependencies.yml file.

![](attachment/acb2bc7ae67984b9d48e786f31e52f5e.png)
So it says no depecdencies.yml file exist but in sample directory in /opt a sample is given, so here's an approach let's make our own dependencies.yml file with a reverse shell and when the script is run we will get a reverse shell as root. Although this approach didn't work for me.

Saw version of ruby for any exploits, version of ruby running is 2.7.4.

![](attachment/a99c0dddb531e146a9bb1a3b6f832cdd.png)
So wrote "ruby version and local priv esc", a blog came which is insecure deserialisation.

![](attachment/606cf808b1518ca9325447a0df7c14b9.png)
So, here it is, we have to write this in dependencies.yml in same directory and then run the script as sudo and it will not check for the type of data being passed in yml file or basically validity of the data and privileges will be escalated.

![](attachment/31ae8edaedf7383231806a63ee862028.png)
in place of "id" in git_set, add /bin/sh and it will give a root shell and then go and get root flag in /root directory.