**ip of the machine :- 10.10.11.11**

![](attachment/2186787179d21c10a7d14126d5b84fc7.png)
found some open ports.

![](attachment/a8649ce777899e5f5e01adbae50eddfc.png)
did some versioning!!!

![](attachment/2d528c4c2361f7a8c9e03f6b0004e8e3.png)
on website found this which means the domain of the website is board.htb which we had to add in our /etc/hosts file.

![](attachment/b60c3b03fbffc8e91c9e2ab471ef9d9b.png)
did directory fuzzing using gobuster and found nothing interesting.

On manual inspection of website found nothing. So started a sub domain emuneration scan using gobuster.

![](attachment/97e317921a8d6b22e067dc1fc580ebe3.png)
found a sub domain. Let's visit it.

![](attachment/cc3b916b6ba32edb3535fac528ce1085.png)
a login page named "dolibarr". So what are the default creds. for dolibar???

![](attachment/afa28fdabb66bca3ce2fb6a9c278f173.png)
admin:admin ???

![](attachment/da3c75908abf7849eebca156d31e5683.png)
was able to login with admin:admin as administrator.

![](attachment/8600bbf57c4fb39b91fa5a90f59366fc.png)
also found it's version let's see if any exploits are present for this dolibar version for reverse shell.

![](attachment/8b07a8c35c6d1e33a8fde6ca0aa1b102.png)
found this. Let's try it!!!

![](attachment/de47e25ff55230145579fc9fbaa91555.png)
ran the exploit!!!

![](attachment/8e776211b5a86dc79f3692c4acf962eb.png)
got reverse shell!!!

Went through /opt directory, cron jobs, and many other files got nothing then thought that it reverse shell'd us in /var/www/html/crm.board.htb, so though that can i find something there????

There were like a ton of directories and files and was failing as usual!!!!

So went to conf directory and found creds. in one file.

![](attachment/24fc1d7143ac21548dc9d8187569905b.png)
found some database creds.

![](attachment/b7d6ee5c6058e85a47a104ab19e93400.png)
found some SUID and GUID permission files.

![](attachment/104a0f1a2a1a7a83625e1e053210f8a3.png)
so searched for enlightenment and found an exploit with associated CVE and further got root flag......................................