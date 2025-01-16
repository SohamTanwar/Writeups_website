**ip of the machine :- 10.10.11.18**

![](attachment/2605112804ac22253b7eb6989a3bbd90.png)
machine is on!!!

![](attachment/0de08ac6e80079755aa2ec036a375f7d.png)
got some open ports!!!!

![](attachment/4de85866e6f91aeaa72a00d9adb42372.png)
result for all the services and there respective versions running on the machine.

![](attachment/f9c1c2223c29e70401e7f37b4454fd5e.png)
found a sub domain through sub domain enumeration of gobuster.

![](attachment/ffb52e8e222422a21cf10d46036aa3db.png)
found some directories through gobuster directory fuzzing.

![](attachment/7da9ab207f226614c43d583f831eb5ba.png)
we can register as a user so registered a demo user.

![](attachment/7198d324a8c4e070e283b276c06d9c74.png)
after logging in found this and nothing interesting.

![](attachment/0c0464e8a40da49da2600272ab7d2f83.png)
nothing else was working as such so went to forgot-password web page to see if we can find something or not.

![](attachment/fbff1945fc62162dae8a1b67e64554ea.png)
Here, tried to attempt some SQL Injection and found that it is vulnerable to sql injection so will be using "sqlmap" further.

![](attachment/132bdf297bc28a55bfc965ee66c1e141.png)
capture forgot password request from burp and save it to a file.

![](attachment/33abfa59e664c56993ddc30154de955c.png)
-r :- file with the captured post request.
-p :- for the parameter which is vulnerable to sql injection
--batch :- no input from the user and using automated ones
-dbs :- want all the databases present
--level :- level of test perform where 1 is default and if it is confirmed that sql injection can be performed than higher level should be preferred.

![](attachment/f95da923ffe3a47fe6d727de71728052.png)
only got three available databases. Will be looking at tables and content of usage_blog database.

![](attachment/c7cc19d86db6a4519ce83612ce50344c.png)
also looked at the possible tables and found "admin_users".
-D :- for database 
-T :- for the table
--dump :- to get the records from a specific table in a specific database mentioned

![](attachment/0d3a4c10b650a0f18f684b1196fa0e5f.png)
got admin password hash.

![](attachment/1f86bea64a0745118f6dbc93e56fcaf9.png)
it's a bcrypt type hash and cracked it using hashcat and password is "whatever1"

![](attachment/21186818db236e9f09b26efd92315a2a.png)
hooray!!! was able to login as admin.

![](attachment/7cc6ac8159822d8da6bd6424c3dafa4b.png)
Then searched for possible CVEs for laravel admin and found one which can help for remote code execution by uploading a php reverse shell.

We have to go to admin settings and then change the profile photo.
![](attachment/56a3741ef7b6649a17469c5edfbc2e7a.png)
it was not uploading .php file so uploaded .jpg file which contained the php reverse shell of pentestmonkey.

![](attachment/840329e8987f7a235db5b1583a3bf6ff.png)
Now while submitting, capture the request in burp and then add .jpg extension to it and then click "forward"

![](attachment/bfcd9c96c500718455fcbec1841eb24c.png)
now we have to use nc and find a link to get a reverse shell.

![](attachment/52d2531c4ffce63c324aa8123ceed308.png)
got reverse shell.

![](attachment/c5c60fc6733b4edc7c66b870b9e9cf02.png)
got 1st flag in user's home directory.

![](attachment/0634036346c4e62e9a39e10cf400fa92.png)
also found another user as well.

![](attachment/6365f06f4c72b7313c13c4980e7d755d.png)
got private ssh key of the user "dash" and logged in through ssh.

![](attachment/9991895a409cc32b1635f0f81483bf63.png)
os info. can be used for kernel exploit later if req.

![](attachment/aad63331a13f35a53241156b6512d820.png)
some services by name .monit something are running what are they??

![](attachment/99df2abfb0964788466650ea4a3a3fdc.png)
saw contents of .monitrc because thought it would be like a config file like .bashrc or .zshrc so viewed it first and got some stuff.
This is password of the user "dash" who is our admin. But password is showing incorrect for user dash. Maybe password is for the another user. 

![](attachment/a1816e10a11e54bd8f78a902757a05e7.png)
was write it is for xander.

![](attachment/1bcd277101d0016463ad44a4f75132f5.png)
xander can only run one command.

![](attachment/c8c694f1c566e8b7c4c3997da09d3aa0.png)
it was a binary so did strings to see what is going on and saw these lines.
So in /var/www/html directory a zip.

![](attachment/23287b60b9f58c46a8dc91c14c88bc89.png)
ran the binary and chose first option to create a backup and it created it in the /var/backups directory.

![](attachment/92f87bfca44cc4253b818d9f6a553feb.png)
Now for vertical priv esc. create id_rsa file and create a soft link with private ssh key of the root user. Because when we choose option 1 while running the program it will create a zip and which will contain all the contents even the private key. Create "@id_rsa" so that when creating a zip after selecting the option it will display private ssh key of the root user on screen only and we don not have to unzip the project backup and manually look at it.

![](attachment/753e8ddfea56afabcdeb0f6445426ca9.png)
it gave us private key.

Now add this private key in a file with 600 permission and then login through ssh as root user.
![](attachment/43565642e22edf4a7a73a08e52ed2274.png)
got root flag......