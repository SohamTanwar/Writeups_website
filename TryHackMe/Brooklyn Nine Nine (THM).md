**ip of the machine :- 10.10.6.101**

![](attachment/129d6f70dea93d1a5f87c4d9de556760.png)
machine is on!!!

![](attachment/4e91d4642ee55379b8bea45a3e36e468.png)
found some open ports.

![](attachment/a45f6b63e52d758579afdf0cc94c0de1.png)
it showed that all are filtered....

![](attachment/925c16bb5377a43ed69dce43296b1084.png)
tried to login using ftp default creds. for anonymous login and it worked.

![](attachment/2b8be34b214bbce2145dd2cdece814af.png)
found a text file and downloaded it.

![](attachment/f9b3c7a5e749d74c82a7a26a030559e5.png)
so jake is using a weak pass... Hmm!!!

![](attachment/42c896c0b3425a07b32dfe32f261b197.png)
went to website to check the src code first.

![](attachment/15b30ed4a43da8b6ef21381a0e43d378.png)
Found this line in src. code which means we have to use steganography.

![](attachment/92996c5f120806f615ebfd88bb3c626f.png)
Don't have any passphrase.....Hmmm!!!!

![](attachment/fd8a948177fdebbd3293a08d52fb939a.png)
So there is a tool in repository of kali which is stegcracker which can brute force passphrase and can also extract the hidden files which is brooklyn99.jpg.out in this case.

![](attachment/77af66fae2692d7b56840ee6b2ecef2e.png)
woo!!! found some creds.. probably for ssh.

![](attachment/765de1c2312738c596087386728b9640.png)
was able to login with id and password and got first flag.....

![](attachment/71a90f18c7b568da40da614681483297.png)
user can only run nano.... Let's go to GTFObins.

![](attachment/36e58a44014186ffa41a496c00e748c0.png)
will be using this way to get the root and last flag further.

![](attachment/e440d12fc01e48ae70e329e7e4057f80.png)
First type "sudo nano" then after entering nano text editor press "ctrl+r" and then "ctrl+x" to enter any command and ten add the payload and you will get the root shell and got the root flag.....