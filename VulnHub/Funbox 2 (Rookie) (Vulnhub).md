**ip of the machine :- 192.168.122.96**

![](attachment/fc845a0ce463faa56b27a1b694de0d11.png)
machine is on!!!

![](attachment/8785455a38e9e1bbb8e9d299c85b1bbb.png)
Found some open ports.

![](attachment/beaf8184d58094eed7cc64ec776a2623.png)
Found versions of the services running as well as anonymous login allowed on the ftp service.

![](attachment/8eb4934087dc846e8e660dc47af82bdf.png)
Also got a message, along with many zip files.

![](attachment/419ac46cacc03efa3c5140c048cad2f7.png)
So, tried to unzip one and came to know that they might contain ssh private key.

![](attachment/cc2c7dc5e4a75e77725be782a534fe2c.png)
So, wrote a basic script to actually get hash of each zip and then crack it using john.

![](attachment/e8cf3f31d0c35d211723419760136e63.png)
Got password of the zip of two users.

![](attachment/6646c00305bd1715c46a18777f33f2e7.png)
So, got two private keys.

![](attachment/a86d27b2ed2cec8e9695e9bda5c51a08.png)
So, tried to login with ssh key of tom and it was showing restricted shell, so at least got a bash shell using "bash -noprofile".

![](attachment/6db83c532b24e33434e83ab46c96c444.png)
Saw in user tom's home directory found bash history and mysql history files and then after viewing them found the password of user tom.

![](attachment/2b6c6eef0d6a7fd592c0f5b750708433.png)
User Tom can run everything.

![](attachment/2e423384c6bf024e7a0d4d6cb5523c42.png)
Got root.

![](attachment/ed2395fb962386595f925ee51046bfcc.png)
Got root flag.