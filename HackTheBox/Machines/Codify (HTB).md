**ip of the machine :- 10.129.1.170**

![](attachment/cbb998086634451923d635776b84ea89.png)
machine is on!!!

![](attachment/dd370517e731135789edb597c62d1472.png)
Found 3 open ports...

![](attachment/29961bb67c32f7cf43b9a7e38dd42415.png)
There are two http servers running...

![](attachment/13c18c60a43e1ebdb29f162d5b668ab4.png)
Added domain with ip in the /etc/hosts file...

![](attachment/e0a8e49a48451926d140e028a02eeec5.png)
Node js code testing website...

![](attachment/8d0e8c87a9dfc391666326f9ecddb132.png)
A library named "vm2" on node js is mentioned which is worth noting in about us page...

![](attachment/6d23d9c0e2f9c1cb51c13c74a6603fcc.png)
As usual which i have already explored...

Port 3000 is also running the same website....

![](attachment/61885d7b1bd17b9651b61cff6724eb06.png)
Every subdomain redirecting to the original website which means no use of subdomain enumeration...

![](attachment/f67e27bf86b208f1304f3c84bcb24abe.png)
Got a lot of security which means that this library of nodejs is actually vulnerable...

![](attachment/787388a1e76714826ac19b7d8bb5632d.png)
Got some example code in the first blog...

![](attachment/8ff0e200bace2f4868aa0cba7bb00121.png)
Ok!!! So PoC code is working, let's try to add rev. shell in it...

![](attachment/3e96a6ce94ec3baa374c71232aca9933.png)
First created a rev. shell file...

![](attachment/ab4b09b3c5bc9859573ecbeb9a24dd08.png)
So wrote the rev. shell payload...

![](attachment/844540d34904664c55987ea4bdddce33.png)
Got it!!!

![](attachment/e1689e5dceaa49b8d44e54f1b6c3513a.png)
Saw a directory in user's home directory reverse shelld as...

![](attachment/6263d6907ec038938e27e6ab4d21edab.png)
Found nothing in .pm2 directory...

![](attachment/3c027fa20915a476e16e37591b464a4e.png)
found another user...

![](attachment/702fcbd00be71f8fb8693b64691f3c95.png)
Got a file in /var/www/contact named tickets.db and searched and got to know that it can be opened through sqlite.

![](attachment/acd74faabdc54c15f6954756b3528c05.png)
So typed sqlite3 randomly and it showed open a file...

![](attachment/c3b9b54fe0d0845090b8468742343286.png)
So just went to list mode in sqlite3 and tried selecting values from users table as it is mostly the default one in most of the databases.

![](attachment/400a6c9ac7dccc02ed1a379dd78f6629.png)
So randomly ran john with the hash to see which type of hash is it...

![](attachment/fc9cad7c5d98c27937dbf1d0f86624ab.png)
Got the password "spongebob1".

![](attachment/d906b5d9a0d2b83374905c8cb234bda3.png)
Logged in as another user and got the flag...

![](attachment/e0b764050a64dcab118c5edf3ec8f353.png)
User joshua can run only one script as root user...

![](attachment/f7bed350c6604912f05a4ef44233be9b.png)
So saw the script's code and it requires root user's password for the database...

![](attachment/145528204a77ef81b008bd9ac8581093.png)
Also tried to inject a bash payload but failed...

![](attachment/5365679f6cd22363ca181bb06b7d03d3.png)
Then saw this code snippet and though maybe a cron job might be running in the background in order to backup the database...

![](attachment/0d848600fc8c38cd1d08bb29bd0553fe.png)
Got root password from the pspy shell as the code for was running in the background...

![](attachment/1c87052772da40911bf08ce229d6702c.png)
Got root flag...