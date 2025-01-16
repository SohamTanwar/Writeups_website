**ip of the machine :- 10.129.229.26**

![](attachment/67e2634a0c9f7bf4dde03ccae4c9852d.png)
machine is on!!!

![](attachment/11d8e384bf467a0e800a694ad025733d.png)
Got 4 open ports but found only two open ports, let's scan them further...

![](attachment/dbf892258f873572f6fefe370d41bc6b.png)
So port 55555 is running HTTP server. Let's view it...

![](attachment/258f44bf0d005acfac251331e839e3f0.png)
Website is running Request Baskets version 1.2.1. Let's see what is it....

![](attachment/ad96723b4881b65057133889f494b00a.png)
So it is a web service to collect HTTP request and analyse it. Hmm... interesting...

![](attachment/73fa339cef24ed78e3eecdae96267824.png)
So searched for exploit and every website showed SSRF (server side request forgery).
So it is vulnerable to SSRF, let's view any article and try to exploit it...

![](attachment/faaf0a0ed00d7cedb7bbf6c512721cb2.png)
Got an exploit, let's run it then...

![](attachment/006d499bf9c63e3bcfb41e78313d4d4b.png)
So exploit didn't work, i don't know why so went to a blog to find how to actually exploit it.

![](attachment/dee54b6c381a4e9b4b11d6c73d9c5978.png)
Got this from a blog and summarizing it, so basically we can create baskets and then request are received in those baskets, but we can also forward those baskets to another server which can also be the server of an attacker at localhost. So actually get the requests coming in the basket.....

![](attachment/8d9b5401212f551da0a981534cb2de54.png)
So used this exploit...

![](attachment/6bf703e706a75ac02ea1c8916385f51e.png)
Ran the exploit...

![](attachment/d7237161fa729d4200de98e5fac8f0a8.png)
SSRF confirmed by forwarding request...

Now let's further exploit it for reverse shell in the server....

![](attachment/470e047132f4750108a924ef370b6bb5.png)
So tried forward URL on my device and it worked, so tried adding 127.0.0.1 and checked proxy response if the bucket is used as like proxy or somethin....

![](attachment/aed5e23b50b35d94da0146ac35fa5bf2.png)
Did curl on the basket after changing configuration and found another site running behind.

![](attachment/8c615abb783c9c617fde45e7b7b5a857.png)
Now opened the basket with provided url and found this....
It is running maltrail v0.53 so let's exploit it.

![](attachment/bb6dda26679e05008b6ef6e46581f915.png)
Found an exploit...

![](attachment/8fe37802c9cd38955fccb17ababa205b.png)
Got a usage example as well, let's use it...

![](attachment/cb5d3870d9e42fede8da09d9f5c7156f.png)
So exploit failed, and then i noticed it redirected to login page...

![](attachment/d4345f9148cefb1866ded9ae67a7c24c.png)
So in configuration settings added /login and then ran the exploit...

![](attachment/ac996c414e1f642b22fc07ac65a5f7c5.png)
Now it ran...

![](attachment/37ee6e34d2999d125681c2612983343e.png)
Got a reverse shell...

![](attachment/91e8b232fe6605f47052c819ee079c25.png)
rev. shelld as the user only...

![](attachment/181718d086b726ec73945d5260394427.png)
Got user flag...

![](attachment/ca49b4d982e21881765a1ceeabc8c948.png)
Woah!! ran sudo -l and saw what the user can do as root...

![](attachment/562f5b9b1f2bf2efc237724c0c51882d.png)
So executed the command as sudo...

![](attachment/475853b15bbed5711c342a560a09a020.png)
When systemctl command was ran it opened it with command less, which is for viewing the file so added !/bin/sh to invoke a shell there, as the command was running as root so got a shell as the user root.

![](attachment/2650d2d0a5afb8e25920786abf09d755.png)
Got root flag as well...