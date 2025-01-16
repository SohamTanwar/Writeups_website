**ip address if the machine :- 192.168.122.220**

![](attachment/6ee470c9d48fc7bb8d0c1c2c4158fcc9.png)
machine is on!!!!

![](attachment/2426dcdf9b28586968a37122650171ae.png)
open ports!!!!!

![](attachment/9ee0b2f703828b3f925b176702e28a97.png)
did a script scan!!!

![](attachment/9e22f4e87479b2ce9adcec4ef92071b7.png)
found some shares using enum4linux.

![](attachment/f902c954d4edb1c450715b8d86db62e6.png)
found log.txt file and opening it in mousepad.

![](attachment/6ae3e699800fb2cab02e06327a19fbc4.png)
it's the samba configuration file.

just re installed the machine and new ip is 
**192.168.122.11**

![](attachment/df0bbd193033a066c82400a1e97d7d16.png)
found password hashes.

![](attachment/075a00febd82f4c4e622aaf0a9211a45.png)
found password for the user.

![](attachment/2682542271e484d06bc1fdb3b5f682aa.png)
found librems.conf file file and seeing that it is running at localhost on the machine.

![](attachment/8440cdc7cb32dc5f9826b5fdec89eca4.png)
port forwarding 8080 of the machine to our local host port 8181.

![](attachment/44f716940f7d6339ece711429f1ad21b.png)
opened it on 8181 and got a login page.

![](attachment/8cc31346f1e93c08a09b1a9ab89ac392.png)
was able to login using creds. of aeolus.

will be using metasploit for further exploitation.
![](attachment/98eacfe72aad8b8f9882ffd8509e9364.png)
will be using 1.

![](attachment/14f142a62dd2a208bcce5555f71fb1f8.png)
set options and enter exploit and gained a reverse shell.

![](attachment/11fe523a297f8bae306a95be19eafeed.png)
did sudo -l and saw that the user can run only one command mysql.

![](attachment/0bb6b108d18d3c9c26678cb62019ad85.png)
went to GTFObins and escalated privileges.

![](attachment/16cf1286a6132476cd22c0602b433e2a.png)
got it............................