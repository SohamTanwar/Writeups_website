**ip of the machine :- 10.10.63.53**

![](attachment/2e096c7be730b4b1ec3cc51e281ac6e0.png)
machine is on!!!

![](attachment/d0dedff2554ad62eec7f7e8b1170a599.png)
Got some open ports, bit no http.

![](attachment/8287b75fb45d4669408d40f04e5bd2b3.png)
So, did an aggressive scan and found that whole root directory is accessible through ftp.

![](attachment/3441a615121e95e5cd35c79a189f9394.png)
Logged in through anonymous login.

![](attachment/ec113ae9760e4e76bd6a5623f79e4551.png)
Found a user in /home directory.

![](attachment/a8934de56c51c46a3aa5065e23c627e0.png)
Got user flag into the system.

![](attachment/7125b1bc5c8ea70e0ad0aff1a3c8141b.png)
So, found this directory in root directory.

![](attachment/5664c074cea4a96af2d5854873fc29e1.png)
Got two files in them. Let's get them and then see what to do with them.

![](attachment/a78fb4f374f8e221e703b1ed6bdcab1a.png)
So, after a quick search found out that private.asc is a private key use for decryption on encrypted .gpg file.

![](attachment/3f0dc5884c3294325ba4c04188f644f3.png)
It asks for passphrase while importing the private key. Let's see how to crack this.

![](attachment/33a28ce8a70256f62c09b9fcb4f9670f.png)
So, using gpg2john to create hash of the private key.

![](attachment/9f25c572b511cae262e4628c0ff7daaf.png)
So, cracked the passphrase using john.

![](attachment/b5edc090e084a4e69973243563e05f6b.png)
It worked. Let's decrypt our file.

![](attachment/ea9242ac2267cd853f7b308d7c0d5dca.png)
So,again it prompted for passphrase but it was same as before and got password hash for the user and root. 

![](attachment/d3865fbb307e95e316fbcf078b432f86.png)
So, used hashcat to see the type first which is md5. Let's crack it now. So, it didn't work.

![](attachment/67ba5356e7b99f7ee6eba7c011731153.png)
So, this time added password hash of root user in the hash file and then cracked it and it got cracked.

![](attachment/da6a5ceb8a34954954ae5ce8459a3d0d.png)
Now, was able to login as root with the password.

![](attachment/ef2d6264418f117017187741d00c1d37.png)
Got the root flag.