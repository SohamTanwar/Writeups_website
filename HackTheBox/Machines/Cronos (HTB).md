**ip of the machine :- 10.129.227.211**

![](attachment/df76112c0a902d068906f7cbfcb6c847.png)
machine is on!!!

![](attachment/cdd951ed8371a4a8dcf2be6d4ca49fee.png)
Found some open ports!!!

![](attachment/1edc44f192dc521bf8e88bd94f0206fd.png)
Let's add domain with ip in /etc/hosts file.

![](attachment/e6e27d6c6e0d3bd31001a44af7c22aa8.png)
Huh!!! Just a normal web page....

![](attachment/f11844ca74b4eaad173c19f1eb1345f0.png)
Found some directories but didn't find anything in them.

![](attachment/9a3896f428d22c53498043c5453b723f.png)
Wooh!!! Found a sub domain!!!

![](attachment/7011ec1922b71025a8c61243ce4617fe.png)
Found a custom login page, let's try the most basic stuff SQL injection!!!

![](attachment/b0d53827f105b852e50b80634a4ffeed.png)
Added the payload...

![](attachment/9a943ad1a52ab3a852fa7fcf9ee19f47.png)
got it!!!

So, I really have no idea what this tool does so captured the request in burp suite and sent it to the repeater to see what can we do.
![](attachment/7f3ff07234413d4d65297a466e382b49.png)
Let's try for the command injection.

![](attachment/32638e9c864537b5dae7866b1a695286.png)
command injection is possible!!! Let's try to get rce then...

![](attachment/40c4e7a9e7763ae3d50019620388827f.png)
It also worked this way....

![](attachment/0950a0c5a19d26a2b8deb99dd0770f9e.png)
Added the reverse shell payload which is URL encoded...

![](attachment/71a7c6396a35e82491a1efe4d5462cf8.png)
Got it!!!

![](attachment/ae8d56670110397b8f4b0587c9e2800a.png)
Went to home directory and found a user there and got user flag...

![](attachment/c6ce27e18b9ab013e287fb72be4ef71a.png)
So will be running pspy to see all the background processes and cron jobs to see if we can exploit anything or not, because no SUID, GUID or writable files found as such.

![](attachment/5c6376af26ed3258b99ce50dd54be412.png)
So saw a php file running in background as a cron job with permissions of root user probably.

![](attachment/47e637aae190a4b137319ba5257872ea.png)
Saw yeah it's a php file.

![](attachment/98ea94e5e294d406cf1b361df4de84da.png)
Saw downloaded the php rev. shell by pentest monkey and changed ip and port.

![](attachment/639fc38b74135093d46e72a0e09b5753.png)
Downloaded the rev. shell on the victim machine.

![](attachment/b11e81a3ca5f144f9c4553f13b3ef042.png)
Sp replaced the cron job file with my php rev. shell file while remaining the name of the file as "artisan" only. Now wait for the cron job to run...

![](attachment/6b81de070d09153bc8b6a40216253064.png)
Privileges Escalated!!!

![](attachment/393bfeb8ad80243fe1e23f8455b4a25a.png)
Got root flag...