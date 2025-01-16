**ip of the machine :- 10.129.232.78**

![](attachment/70a0313624b570e65af759708f0e8a06.png)
machine is on!!!

![](attachment/1fe3b1c0c0fc575df80ff6022af9829b.png)
Got two open ports!!!

![](attachment/e004a8b83fcc3535b3c3bc12ff54cb88.png)
Let's add ip and domain in /etc/hosts file.

![](attachment/4e407310d050e71edfba6e27a3ca1a59.png)
Let's see the website now!!!

![](attachment/818f7ea030466532a5b25443afe2ccd2.png)
Found nothing as such...

![](attachment/6a2665b53a1e67d845167e0ade5e5d1f.png)
Found some really cool directories to look into.

![](attachment/237f4db7af7b47a2986542e0983dab16.png)
/test directory show configuration for all the web pages on the web application which looks interesting...

![](attachment/9ad7126cbf159a8f998583ef442c6271.png)
/torrent contains a torrent service hosting.

![](attachment/9152a38cef1ac8266ff226c26457da6b.png)
It asks us to login whenever i try to go anywhere in /torrent and the service that is running is from 2007 which means it may have some vulnerabilities and exploits along with some default creds. Let's check it out...

![](attachment/76059bbe3e7d048687426064cd1a1c86.png)
So found a file upload vulnerability exploit with some steps to follow and further get a rev. shell. Let's understand it...

![](attachment/b3af2c8402267206c8b25be99bc6d3da.png)
Let's do a common php file scan to learn more about the php files in /torrent/ directory.

![](attachment/15bce05d3d4ea3f365eb2895546e7255.png)
Oh!!! Found a lot of php files including the upload ones, as we know it is vulnerable to file upload vulnerability...

![](attachment/f79a5dc5389494c6262bfb5de9d3fb2e.png)
So every page is showing this blank stuff, I think so we have to login first but it doesn't has any default creds. Let's dig more to find any other exploit.

![](attachment/af7d158b63092d1522fdd3d86efe1125.png)
So after clicking on upload, it is redirecting us to the login page every time so will try to bypass the redirection. So yeah it didn't work as well...

![](attachment/4e7a08d19d97e3c3c9dae99b285c86ed.png)
So logged in as the user "test". There was a signup page, so i made an account with user named test and now i can access upload page to exploit file upload vulnerability.
![](attachment/6550fb08e0f9b64b3ce971b663bfb5cd.png)

![](attachment/3ac83f0d293e59a808c81dfc379a5571.png)
So downloaded pentest monkey reverse shell.

![](attachment/399e6dd05878d962e326dbd544e4e4fb.png)
Added all the required stuff, let's upload.

![](attachment/5943b9985a0cb25369b01bef1f18e8af.png)
Of course it wasn't, it was a .php file. While uploading let's capture the request and try to rename it.

![](attachment/03717264b9611f0268787c4f76909127.png)
Let's change it to .torrent after .php.

![](attachment/b12762a431b9819c064aff91edc42c79.png)
Again it didn't work, let's see the exploit that we found on exploit-db again.

![](attachment/02bcf85272a45b737f116125f4ae783c.png)
So renamed my file in the system and now let's try to upload it again.

![](attachment/d76337d45eab66f2e8109eb10e693618.png)
Let's try to capture the request again to see whether it will upload or not.

![](attachment/17143d12aa72ff50eb3fa6e0ec2f9e01.png)
Previously, it was detecting that we uploaded a .php file, now we are uploading a .torrent file, so there seems no problem now.

![](attachment/00dc502a5cb6e03c8f2fa33ad0fcbbe3.png)
Still failed...

![](attachment/1a86b1b2d50bcfedaf3735045032314b.png)
Now this time renamed the file with a png extension along with php.

![](attachment/0dccfd2d16a9c4e060b28c8351f5aeaf.png)
Now after capturing the request changing application/php content-type to image/png.

![](attachment/cd084a789474e1ee1ff6094d878209c7.png)
Still not a valid torrent file. Is it even accepting the torrent file or not.

![](attachment/f68b69a33ec3260567fc8de1b3364d2a.png)
In upload directory saw .png files which means it is accepting .png files.

![](attachment/2874423c78d84bbcedcff56441876b55.png)
Maybe it's not the place to upload the revshell as it needs a .torrent file, so let's the one available on the website.

![](attachment/53a965365d8092cfff382f37a651411f.png)
So uploading a kali linux .torrent file that was on the web application itself, because upload directory only has the screenshot of the torrents and not the .torrent files.

![](attachment/b494826a9db7c36c8f971e4e30c1f826.png)
Let's get ourselves new torrent file.

![](attachment/e937646792600b86395d1c65b1c8e7e6.png)
So downloaded bittorrent file of parrot.

![](attachment/a6c67e07e10b334f487336c2f316c791.png)
Now it asks us to add the screenshot let's add reverse shell here with .png.php extension.

![](attachment/c2bbe4e905448c78dab1054ea0bb2e7a.png)
Let's add our screenshot... I mean rev. shell...

![](attachment/f5eb6150d8f4989b0e060d83e6079650.png)
changed the content type of the screenshot.

![](attachment/7659df4c9954f52da060cae1ebbc33ae.png)
Wooh!!! Uploaded...

![](attachment/59a4c55739d31cbb9e2cec5cc6c9bdcd.png)
Got it in the upload directory.

![](attachment/590aa1c80bf341b1b7cff620550332e0.png)
Just click on the rev. shell and got it!!!

![](attachment/aac0c1fdc196eb38a7809e1c4de2cd2b.png)
Found one user in the home directory and found the user flag...

![](attachment/520c5ad1dffd914dfc30003ef63f92c5.png)
Found database creds. in /var/www/torrent/config.php file.

![](attachment/01747230a6f4aa3d46bf21b6c4bd673c.png)
in the mysql database with the creds.

![](attachment/c64f1da147afc00b4bf4d0efd77aea25.png)
In, torrenthoster database, found a table by the name users and got the admin password hash.

![](attachment/9c0929634f259e824e3279eb281145d3.png)
Hashcat was not able to crack the hash and not even crackstation.

![](attachment/0d0dc9fe8dc521a9aa3c9822ac6c711c.png)
Didn't even find any .ssh directory or private key in order to login as the user.

![](attachment/e7022f46cccf02d8fc7637028f2e9b99.png)
After finding everywhere and trying numerous things, went to user's directory again and noticed that we can see only one directory .cache. So viewed it and found a file with an unknown name.

![](attachment/87ad042df889cacdf45c2ea9e7f6bc27.png)
Oh!!! it is the message displayed to the user, every time they login through ssh.

![](attachment/5451369241e521acb0d4a99a9c878d7b.png)
Then found this on exploit-db.

![](attachment/97cf6f0340bc895f4176b07ac4aa9115.png)
ubuntu only!!!

Let's try this exploit then!!!

![](attachment/d18b562d1501866964cc9d8085e84ac4.png)
Got the file in the compromised system. Let's run it...

![](attachment/b2b1a6b0628f629829fcce776d3b0e3e.png)
bash is showing the error. Some google search revealed that it can run in sh.

![](attachment/cb2560b83268a13f88715d28415fc755.png)
So, the exploit is not running...

![](attachment/05b124dc1a6cd7ea1fa34e5a818cfb6a.png)
Let's search for any kernel exploits.

![](attachment/1d26120f75f6642d250f1b78f5cd0fb6.png)
So ran a kernel exploit!!!
![](attachment/612b434bcf17e1c1f1408aef1073dda7.png)
The above one which comes under dirty cow vulnerability.

![](attachment/e8c366f76bfdcacaac228945aaa42543.png)
So this exploit created a new user with a password displayed in /etc/passwd file and it's home directory will be /root.

![](attachment/74d0d5edebdb7138c50618d4253d357a.png)
So when the exploit is run, it asks for a password which i set "toor" in this case and got root privileges.

![](attachment/6513d8abfdf189cdd1e1cea5657baa5a.png)
Got root flag...