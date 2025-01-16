**ip of the machine :- 10.129.228.109**

![](attachment/771df59888beb53df43887bff6c47ddf.png)
machine is on!!!

![](attachment/28415bfbb95650d8a4855dcfca19d48b.png)
found some open ports... but found some unknown ones which seems unusual.

![](attachment/e3f09244921af11ebaf38ff11f67627a.png)
Aggressive scans revealed some versions but only ssh, http and nfs are of use or worth.

![](attachment/267258e0bfdfb4f3161fa2f3076ef344.png)
Found a website but didn't find anything worthwhile.....

![](attachment/b84a74582a6b0c91d99d5b3261bd786a.png)
Found some directories and then visited each of them and can only see there files but nothing interesting in those files. But the only good thing is we can see them that's all.

Now let's start with NFS (Network File System) which is networking protocol which defines how files are stored and retrieved.

But there is something about network file system it contains certain directories/shares which we actually mount in our system and can actually access the files in those directories, so let's see what possible directory names and shares we can mount... For this will be using a nmap script...

![](attachment/4fb47bb9fdf04d02ff60932e608c7cc3.png)
So these are the directories/shares we can mount. Name of the script is "nfs-showmount" and can be found by a simple search.

![](attachment/f05fefe0871dd5806e3d34a6c133a3d2.png)
So created directories in my /mnt directory to mount the file system.

![](attachment/e9fd2486a32b9d1557a439c04a0d4581.png)
So used "mount" command, "-t" stands for type which is nfs in this case. So mounted both in my system /mnt directory.

![](attachment/42108758795f822e1c159efb7fdaa745.png)
So this is home directory of user "ross".

![](attachment/1a5d72c41a1c0bc31ee8909707029fe3.png)
Found a .kdbx (which is a keepass file) in the home directory of the user but it also requires a master password to reveal the creds. which we don't have it....

So for now ross user home directory does not require more enumeration so will be going to /var/www/html which is the src. code of the website running on the web server.

![](attachment/17eec497d5b2008045c15f01ee362ea3.png)
wooh!!! permission denied so did "ls -al" to see permissions of the directory...

![](attachment/450cea79de40e550b9b95cd56cdce01a.png)
So, mount_2 or src. code of the website can only be accessed by a user with uid (user id) 2017 and group name "http". So let's create one shall we???

So this is one of the weakness of nfs shares when mounted in a system, we can create even user and group with custom uid and gid in which share is mounted and access files and directories which are not allowed to access upto certain extent.

![](attachment/9af7d52485eb93ebd9c2b1b4f298b3ba.png)
So we made a user by the name "abc" with uid set to 2017 and adding abc in it's secondary group http.

![](attachment/0d13600e1cb942e47e488fb8960c3755.png)
Now we are in mount_2 or source code of the website directory...

![](attachment/57cc6d6132d11260cda6c1b3cc0c1355.png)
The user we have created also have permissions to add, alter and delete files from the directories...

So here is an approach :- let's try to upload reverse shell in the images directory specifically php reverse shell by pentestmonkey and then will go the images directory and then try to invoke the reverse shell.....

![](attachment/ae493be1cd995a7953930256cc7010ee.png)
Added it in the images directory...

![](attachment/c71ace368175e5878c539363726b9785.png)
Started our nc listner.

![](attachment/070e1e60fa188577ebef75dc358eecbe.png)
We can see revshell.php, simple click on it and you will get reverse shell.

![](attachment/6d4f0e0a762befa5e2de7aefcd24ac56.png)
got it as user "alex".

![](attachment/73e47efabeb7906bebbe471b81cbfb17.png)
Got first in user "alex" home directory.

![](attachment/085f4c9c08e034add86ac8744779db05.png)
Now after enumerating different files and directories for a long time, saw a file named ".Xauthority" and wondered what is it.....
So came to know that this file stored credentials for the authentication of the user for X sessions like (X11) and also contains the data of user done in a particular session just like session cookie in websites, well a bit similar to that but not exactly the same.

![](attachment/93ac8eec9d5148456185bf4a67fd3415.png)
this file is in the form of binaries so cannot read it, let's make it's base64.

![](attachment/fbdff4a91b97e044cc5884b9273068aa.png)
Created one. Let's go back to attacker's machine.

![](attachment/5ba9922e3e8f9ea0fe4a8ff3ec399e52.png)
Added it in a file and then set an env. variable to set a session and we can see session is started as user "ross".

![](attachment/a9fb03d4d4b33a5a59d4b672a18bb59f.png)
So now will be using xwd command to actually capture the window of the session.

![](attachment/250e0ce6c0da0a9d52082d1ae85d63e9.png)
So used xwd command and then redirected the output to an .xwd file.

![](attachment/ac1807dd384e77be1f9729ff3ece55a6.png)
So used nfs to share file with my system...

![](attachment/1621b97180d50946105bd73029b989ac.png)
Went to an online xwd file viewer...

![](attachment/db879f561ac3f15972e126b2ad50f957.png)
After uploading .xwd file on the website we can see password of the root user.

![](attachment/f3527280231a788202d83fcf0109b255.png)
Logged in as root user and got our last flag.

![](attachment/9150e971fc7fdfb72badb484571398d3.png)
At last to unmount the file shares or shared partitions use "umount" command and to delete the user which we created "userdel".