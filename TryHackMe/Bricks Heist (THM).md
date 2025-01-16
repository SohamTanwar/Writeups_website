**ip of the machine :- 10.10.94.0**

![](attachment/f46407435c6d289e19a4b6f1adf456c1.png)
machine is on!!!

![](attachment/13f277643f7f269046134a8095151071.png)
Found some open ports.

![](attachment/0d01c582faa8c3bc369b27c5a353e2ce.png)
did aggressive scan and found versions of services running on the ports.

Gobuster was not working, SO used ffuf for directory fuzzing on port 443 (https) server.
![](attachment/6097122898cd37051f107a11070de0da.png)
Got some directories and mostly redirects (300s).

![](attachment/31bda952f692cd78622d034622f3bcd4.png)
Just thought of going to robots.txt which is like a default file in almost every server and here we can see it and predict that wordpress is running.

![](attachment/7d59ee79125836c4f4bc4702f24f15aa.png)
found the login page

![](attachment/08e8fa19400565adce01b38f981a7ea8.png)
when entered /feed it downloaded a .php file and found a possible username "administrator".

![](attachment/2b887536c225b69bf44d2a603e3b4d72.png)
at /phpmyadmin found another login page.

![](attachment/54dc06d1676fcf58dd5f433de477c0f5.png)
nothing worked but got an idea that it will be used to access mysql server.

![](attachment/4065287ef818e745e6f5f0e1b25b674b.png)
password was wrong but atleast the username was right.

![](attachment/d44de72a11454bf8ccf70d4243e9f4d5.png)
now wpscan worked. Earlier it was not working because of checking of tls certificate.

![](attachment/a4c0334e74a78f1e487d58a686a1a5a1.png)
found this a bit sus!!! so did a fast google search on bricks.

![](attachment/f452c21cd4bfd43b5d2e0ab9b721590b.png)
found wordpress bricks theme to be vulnerable.

![](attachment/4840340e7906f54a5b03cef4f29f2522.png)
So after reading about this CVE, it is basically an unauthenticated RCE vulnerability which can be used to execute php malicious code on the server and is in the Bricks theme of wordpress.

![](attachment/875bd0b82a0ad3496a48c678404fc02c.png)
So used the exploit given and in the server.

![](attachment/23b532945898540c42db0fa691a3c601.png)
added a reverse shell because cannot run many commands on this shell.

![](attachment/de96755ec980161cf866528b0e62c66f.png)
got reverse shell.

![](attachment/8e3f27301942c3b2921fa0ae780e1cc0.png)
got some possible usernames with bash default shell.

![](attachment/9095623dc98af5de9018db078563e43a.png)
got some info.

![](attachment/a9917eaf1f655ff874533be153e49b0d.png)
did rev shell again and saw some Wordpress php config files and found this.

Before doing rev shell again, saw that user "ubuntu" home directory can be accessed and then found lamp.sh in Downloads directory.
![](attachment/bb6cf9e4ea05de5082bc2bfae7dd8d8f.png)

![](attachment/eeb65f5a09de6aa16d105b76d84e05de.png)
Hmmm!!! used for installation...

![](attachment/47e688fc30f654ab54df8b16fe6f7c9e.png)
used this systemctl command to list the services running.

![](attachment/be583a98befb48197739853cd6baea2b.png)
found this service suspicious.

![](attachment/55580f1b9ad24000bf3e258741044d54.png)
above command can be used to view about a service.

![](attachment/e33168b37d1ab1c9998b7d88240da8a9.png)
we can see that in that directory where service in running, there is a config file, inet.conf and has totally different permissions than other files.

![](attachment/6f7d77f726c4aab1fcd1dc34dc15891c.png)
mining!!! what crypto mining maybe. What is with ID though???

![](attachment/05df8048b158975d47267541486e4e6c.png)
it was two times base64 encoding and it was like two times.

![](attachment/a8ff43a3c6023464a1f9c3458b5321b0.png)
didn't what was decoded so copied whole and pasted it on google and found it to be a bitcoin address.

![](attachment/a555aa5ca90ae572ad576168a0845379.png)
went to blockchair.com and enter address there and saw transaction and got sender and reciever hashes.

![](attachment/a70c4d3b18eb59c6c6ff718b43d4aafd.png)
got some websites and came across a name.

![](attachment/8ccffb10a1a02045caa6231666c2ccc1.png)
who the hell he is???

![](attachment/9f8520fcca79e39c13317700d4336faa.png)
then searched his name and got to know that he is the creator of very famous lockbit ransomware.