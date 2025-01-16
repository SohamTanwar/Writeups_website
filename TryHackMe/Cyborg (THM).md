**ip of the machine :- 10.10.208.132**

![](attachment/8ab17fda7ac9da43ce129ab4a76c9dc6.png)
machine is on!!!

![](attachment/d67e24bd16765739b5d803ee078f0f3a.png)
only two ports are open.

![](attachment/e41e0d693857c86f6810a817f0ba3ee7.png)
Did an aggressive scan and got to know about the versioning of different services running on the ports.

![](attachment/ab1ed7ab7afa3d0d015dcd073cb10ddc.png)
found some directories, let's look them....

![](attachment/7fcbaa7df5553aaa08d59abf3aeea214.png)
/admin, let's further look this directory.

![](attachment/252fac0a056cd8b2f2036fd1b8c4ad2b.png)
in one option found an archive and downloaded it.

![](attachment/b9588c539632d36aecec5ad30ffdfdcc.png)
also found admin shoutbox in admins web page.

![](attachment/5ead20164c5dfe02d5de99f4cfbf9b9a.png)
in /etc now...

![](attachment/e260da6be7af33f3ea263330d4c593e8.png)
got a passwd and a .conf file. Let's see the contents or download them.

![](attachment/d5f78cbc9ff485716beb108fb1980ec3.png)
got somethin'...

![](attachment/5994857b18bd3b4451eedcbc4934a089.png)
what does this conf file mean!!!! It seems like an auth config is connected to /etc/squid/passwd in order to authenticate. Let's try adding these credentials for ssh login.

![](attachment/83d905efd796fc07229b6e0a8030c840.png)
was showing password incorrect so went to hashcat hash modes and added apr and saw that it is an apache apr1 md5apr1 hash so will crack it using hashcat now.

![](attachment/5597bc0325a7effa4f24c8c0ceae832d.png)
so the password is 'squidward'.

![](attachment/2bdd50ece916a7fcbe3a58732c8bd60c.png)
maybe this isn't password for ssh login then what then....

![](attachment/36aed1336b3f195a58923864df613110.png)
Extracted the .tar file and got some files and sub directories.

![](attachment/98c8077861b3ec266ce2573a3a1db7c6.png)
so there was a README file and got a link to a documentation.

![](attachment/e5f108ca8fb6e928355d43988984d9eb.png)
So basically borg is used to create backups with encryption to even make backups secure.

![](attachment/607ca51f149817ff7491c3d168a0bd87.png)
in this first we have to mount our archive somewhere and then it asks for a passphrase, which is the one we got before.

![](attachment/12758934a1491e154156988905583f56.png)
we got a new directory and some new files.

![](attachment/d45137ca96699daa1ab950b8a336a389.png)
whooo!!! so in encrypted archive backup, it is user alex full home directory.

![](attachment/316b912f11e7d28204106b93b8257a3c.png)
in user's Documents directory found a file with some creds. Now let's try to login through ssh.

![](attachment/542c93eac07ade23e793409801c2e193.png)
was able to login as user "alex" with provided creds.

![](attachment/0afcb006758b854104394427c406fd81.png)
got our first flag....

![](attachment/8c68ed9ca0a5a7652be3e3ec2a9e3990.png)
i saw that we can edit the file, so added bash binary/shell in the file and ran the file as sudo and got root/pwned shell, go get the last/root flag.