**ip of the machine :- 10.129.3.216**

![](attachment/6d968e308ed5e422c59727904e6e3fd0.png)
machine is on!!!

![](attachment/6e7de537ad07fc493c00229b8b424fb6.png)
only two ports are open!!!

![](attachment/a46d4dbd29d9a076bc3fade2a05b3507.png)
Got versions of services running on both the ports...

![](attachment/1bf7ebea1b6d66096116924a41c0483e.png)
found an index.php file through directory fuzzing not else... Let's see it...

![](attachment/b5b9f1105eef5c60e9fccfc67ff6eadd.png)
just the same as the default one when we add ip addr. simply.

![](attachment/8a40339f80136380513423723b817b8f.png)
Then i analysed the response headers and found PHP version 8.1...

![](attachment/1d9b952c83497e89b53ee83a6a985837.png)
found this exploit of version 8.1 of php, let try it!!!

![](attachment/452a1c82f5f9abff34ef46c614694f17.png)
ran the exploit!!!

![](attachment/a3b34ca6e2661540e5b3a392234c6d7a.png)
got rev shell as a user...

![](attachment/8f988cdde004cb1b838ad317929f347b.png)
simply went to home directory of the user and found a flag over there...

![](attachment/21ceae5ae6ff9f8e893db94974886fee.png)
by doing "sudo -l" found that user "james" can only run one binary as root user.

![](attachment/2ad3edfba6a452e8ff1a9cf8f6efc2b7.png)
Got the command on GTFObins, let's try it!!!

![](attachment/7b05077350b06845068f3350ba530360.png)
entered the payload and escalated privileges vertically and got root flag.