**ip of the machine :- 10.10.11.25**

![](attachment/ff54871aa034e506a751a76d0b4dc8cc.png)
machine is on!!!

![](attachment/f6ba91c9715c05ec871b1448af6d13b8.png)
open ports!!! But port 3000 is running ppp. What the hell it is??

![](attachment/90b7f40d659c0948ed9c0eb32a893f40.png)
after an aggressive scan found nothing as special as expected.

![](attachment/12c1e99c09bb8649a7b0b03eb30aecdb.png)
port 3000 was looking a bit and the aggressive scan revealed like a web server is running so visited it and found it but will explore it later after doing some directory fuzzing and sub domain enumeration.

![](attachment/269613e227985ea0b6d4007a7cdbf5a8.png)
was trying to do directory traversal and trying to view a file because directory fuzzing was not working with gobuster as after opening website at port 80 it redirects it to a file with file parameter so tried to do it.

![](attachment/bef5ee623fcfee5b8789a4e318d11b13.png)
Didn't find any subdomains as well.

![](attachment/ccad9d4e01fb936caaf2e20fae5f29bf.png)
So at port 3000 one there is a sign in and register account web page, now already tried sql and xss and nothing worked.

![](attachment/d16104d6f630f68ea4da5664e97f47ef.png)
So entered with some dummy creds, which created during registration.

![](attachment/4fa762ae105de9a3f9279e49271fb684.png)
in explore section and then users found a possible username "GreenAdmin" and in repos also find a repo by GreenAdmin.

So in website source code in repo section it was showing many web pages which were not being displayed in gobuster scan so tried to troubleshoot gobuster and then the scan worked.
![](attachment/dd89f977f33f2c0ca8fee42d6b8ae1f1.png)
found some and now let's further analyse them.

![](attachment/8008edf80cbd4cced411de884027b948.png)
when went to admin.php, it said to login as admin and enter the password but what is pluck?

![](attachment/844169ad5d7e6f0efcb339c8351204d6.png)
pluck is also a CMS.

Let's first search more directories and webpages and then will try to look for any CVE for RCE in pluck.

![](attachment/a475da7d74c5c646012cffca57d7997c.png)
two dirs huh!!!

![](attachment/6babd005f6749cc083fd41948410eaf0.png)
was unable to access /data/ and /docs/ directly through changes in url so went to repo and tried to see some things there and found more info about pluck cms which can be helpful to find required exploit.
![](attachment/4428bf2e08f253f2379d28b7c06f795a.png)

was unable to use any exploit so went to the repo and tried analysing the code again and specifically login.php because it is redirecting to login.php and only asking for admin pass.
![](attachment/16c134fff388c108e8b5027d7fc35311.png)
it will encrypt password to sha512 hash and then compare.
![](attachment/dd9e3015aad48708049e2569c0d7b30d.png)
it will compare the password here with ww variable which contains the hash probably so let's try to find this variable.
![](attachment/9fbf3dd2ec85094a361058ac1ad1cc76.png)
found the hash!!! Let's crack it.
![](attachment/c1bf44a378b63700fcc062097919c591.png)
FOUND it !!!

![](attachment/1e8b038edeff35c35e62b24400e46844.png)
logged in as admin.

![](attachment/832ac1e67ee4a222f3efabced65a9678.png)
followed this exploit and then added reverse shell in the form of .zip as it will be extracted at the server and then executed there.

![](attachment/ca83320cd39f98286e25af7e0651280f.png)
got reverse shell after uploading .zip.

![](attachment/0e1a167b1941e07afdddfff312254259.png)
got two possible users.

![](attachment/0f975bcbce54a1a1776852421ff4930e.png)
did password spraying and was able to find that user junior is using the same as pluck admin.

![](attachment/4b903b75f20a42228af69de49411a9db.png)
got user flag.... as well as a pdf.

![](attachment/20bc4385464dcc53e632c236aca3cf3b.png)
so maybe openvas is the key to sudo i guess!!! but what is openvas??

![](attachment/f3ec0cdf4138a089ca16235fc3fe4898.png)

So we don't have to use openvas but if we notice that openvas is a part of sbin directory (system binaries) which means it can be run as root only as junior has no permissions. So maybe the blurred password is the root password we want.
![](attachment/91d9f49bda3294de373ec5af8b36f4b2.png)
Now we have to use a tool to clear the image and reveal the password.

![](attachment/da9c868dbd0b02a9b1287fd983d43064.png)
found this tool, so will try it!!!

![](attachment/3a8969e7c8eae1d187e35db0885815b4.png)
already done!!!

![](attachment/d95c3e8b6f5728100c989d4f9d5a0ea9.png)
got it!!! Now let's login as root!!!

![](attachment/bb2bc12c567c58eba860d041b44d980c.png)
got it!!!!!