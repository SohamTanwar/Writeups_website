**ip of the machine :- 10.10.227.58**

![](attachment/d391c052cbb80f20494d3752b88d8368.png)
machine is on!!!

![](attachment/0a743e31166cfef4f7f300222dac6ba2.png)
found some open ports.

![](attachment/82579e358e72ed6c077e8ac1a56e7c03.png)
found a web server, ssh and SMB running at default ports.

![](attachment/5334f639d7c803815d8dbbfbec62db73.png)
found possible SMB shares available.

![](attachment/1426a46399ed4ebec299fec2edf9cc66.png)
was able to access a share but found nothing. So now, will go for directory fuzzing using ffuf.

![](attachment/70085a9dd3ea7de12863874f7a4e7c52.png)
found some directories we can explore.

![](attachment/e8e9360e05a50254ab9b08c19ca40516.png)
when entered url, it automatically redirected to a login page.

![](attachment/0ed6f962c1f288469bb8e31e9fbbad4c.png)
in /cloud found a place to upload using external url. 

![](attachment/1d18a33981add0d56827707c5e33155a.png) was able to add an image using local server on our machine so let's try to upload php revshell now.

So uploading .php will directly give error or will basically not give revshell so instead when adding the revshell, add #a.png in last as after hashtag it will ignore everything and it will accept it because of .png.
![](attachment/b8cc2330b0041ebeea8207ca6de47ef7.png)

![](attachment/4b02a8007988a6bec92aadb5fb9cdfee.png)
found a user.....

![](attachment/b04c2b11ac3526259fd26c357576dee0.png)
sysadmin has our first flag but we cannot access it.

![](attachment/b10e495b31c42e6ee673cbf8240e6ab7.png)
So went directly to /var/www/html to see if in the login.php file we can find any hardcoded creds. or not and guess found one!!!!
So discovered a login page and let's try these creds. now. OK was wrong creds. didn't work i don't know why.... Let's search in some other directories like /opt, /dev etc.

![](attachment/d66cc4fe9274e9b9247991281a35c5e0.png)
ohh!!! found a file in /opt directory, so gave a search what the hell is .kdbx.

![](attachment/1928f334e8db2c6806d24b067b75d620.png)
oh!!! it's a keepass file. Let's transfer it in our machine and find some passwords.

![](attachment/f5cfd8be2cffbd2e8991e2d6e299946f.png)
found this how to crack it, so will use it.

![](attachment/8b856fbc04546fc2b43db0f199bf6a37.png)
found it!!!

So tried the cracked password to login as sysadmin, but it didn't work.

![](attachment/43fef3b92097cd5f407f266d3b366fad.png)
So came around this article and it said that the password we have cracked is actually to open the .kdbx file using keepass2.

![](attachment/db90b5e6446fe9b4ea6e18594655137b.png)
Got a password. Probably of sysadmin now.

![](attachment/3d4782c9fde945d6323b1568a121f223.png)
Got it.. and then get your first flag.

![](attachment/6288811af1e4ec6b33c47a27ffb6ddb7.png)
So a script.php file is controlling a file named backup.inc.php from the /lib directory so if we add a revshell in backup.inc.php then it will give us root shell.

So in order to edit the files, logged in through ssh.

![](attachment/27dc4e1f52f82499aa3592daa2e7eef8.png)
so added a revshell.

![](attachment/0a76ba7a6aac9a09a7767ae8c4fc1b4e.png)
tried to do some random stuff in order to interact with the file.

![](attachment/521b4090044af608bd225f199b4397c6.png)
got root shell and got last flag.....