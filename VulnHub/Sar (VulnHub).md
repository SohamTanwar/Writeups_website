**ip of the machine :- 192.168.122.27**

![](attachment/9f4a5f02e71cdecc62ef756905dcc92b.png)
machine is on!!!

![](attachment/242e71df32efc12a2c771ae673a9b0b5.png)
Found one open port.

![](attachment/c10329be07ef43f238be2231772363f4.png)
Performed an aggressive scan to get the version of web server running on port 80.

![](attachment/3433b06ff15263a6ce5a584c8948d027.png)
Just the default apache page.

![](attachment/f687070975e365ef40370cfa4b06f459.png)
Found some directories and files during directory fuzzing.

![](attachment/ac21168bbfcbad9251b0d97ac0d9345a.png)
Got the name of another directory in robots.txt file.

![](attachment/0fed4fefd965ac457667c8011d5dfacb.png)
So, sar2html is a service that is running on this web server.

![](attachment/80d0b6f146438d7b4f71314fee0a52dc.png)
Also got the version that is running. Let's see if there are any exploits available for this version.

![](attachment/2d040c4537a204647b2559bdc14c6ff4.png)
Got a way to get initial access to the server.

![](attachment/892455c97ea8cd166884691b5763b9ca.png)
Let's try to use it!!!

![](attachment/ae6686dcf33921c4555a73f1446d9071.png)
So, it said we have to add ";<command_>" in order to execute commands, so trying id.

![](attachment/290a7c877bbc6e24650bbae1bb36fb91.png)
Ok!!! it worked. Let's try to get reverse shell.

![](attachment/90336e659a237341b7ecaaa4d4da9413.png)
So, added the reverse shell payload, but it won't execute like this. We have to url encode the payload.

![](attachment/bc30dcfab10a62242ca2eb526a1c193d.png)
URL encoded the payload.

![](attachment/aef12bcf4938665de4dc911e9d29f830.png)
Got reverse shell...

![](attachment/f23d34c9e9c4fcc8d1d52670aec50124.png)
Found nothing imp. in the directory in which reverse shelld.

![](attachment/71cec765b6b4e3a36772f27e7c00168d.png)
But in /var/www/html found two scripts with permissions. Let's view them.

![](attachment/28a4368ea8d4aa3f7cfbb3d64fea3235.png)
Ok!!! So, here in finally.sh which can only be executed as well as read and write by the root user is executing a file write.sh and write.sh is the file that we can edit as the current reverse shelld user. Let's see if finally.sh is even running as a cron or not using pspy.

![](attachment/a1792fcd990a580d6fca07a47b6c1247.png)
So, went to /etc/crontab file to see whether the script will be executed as a cron job or not as it was not showing in pspy then came to know that it does run after every 5 minutes!!!

![](attachment/613e2f677e72285994d34bf2a8f58618.png)
So, added a reverse shell payload in write.sh.

![](attachment/a4db9a354780fa453173f470bea2ceec.png)
Now, let's wait upto 5 minutes with our listener.

![](attachment/f35c7e0a524745628dc4e2e1388e350a.png)
Got user flag in user's home directory.

![](attachment/a9f1a1bfe0b8f57ffb6d389c7ef1c72b.png)
Also got root flag after getting reverse shell.