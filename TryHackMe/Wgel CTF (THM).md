**ip of the machine :- 10.10.174.152**

![](attachment/68e1532be2cea86ab79f71e86858f147.png)
machine is on!!!

![](attachment/4e14a7fd181cad287a4d376acd9c8236.png)
only two open ports!!!

![](attachment/c04328b67186bc661e8ec7a15d284ce9.png)
did an aggressive scan and found some versions of the services running.

![](attachment/ce21e2749fdfc6f828ea3b188e431e16.png)
got some directories....

![](attachment/d1e44280ad61e5cc4cc1f23b5d335621.png)
going to the only directory we got, and got an application running and was unable to figure out what to do manually, so decided to directory fuzzing further on /sitemap directory.
![](attachment/ec608cf8c0446099728dd0c68c1df523.png)
wooh!!! got .ssh.... Let's see that....

![](attachment/80704d4acd1b918cbdaff04e1a3be593.png)
got a private key to login through ssh.

![](attachment/aa57cf9cf401a3a048437193fbd25497.png)
So was finding here and there for a username and found one on home page itself. "jessie"

![](attachment/61d53cef435c85aab8173043e2b44497.png)
was able to login as user "jessie" with the ssh private key.

![](attachment/9b306b2e67aa624d8c2b3f57a48a2481.png)
found first flag in user's Documents directory.

![](attachment/54cc1ddd80ea70eb4e0702ebabfd6f37.png)
user "jessie" can run wget command as root user with no passwd.

![](attachment/ef3180eda8d62390ba8c59dcec0c3300.png)
To exploit wget to get our last/root flag.

![](attachment/fb861937e26b1f3c7c5ccdc6bb9af7b9.png)
sent the flag through wget to the open port on attacking machine, and got the last flag.