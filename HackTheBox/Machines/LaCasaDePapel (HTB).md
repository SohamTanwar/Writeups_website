![](attachment/05446fd1d79648d2bc79ad9bfb3d2931.png)

**ip of the machine :- 10.129.69.102**

![](attachment/8d55e6341448af21f785287d15a3dd4a.png)
machine is on!!!

![](attachment/d731b172f2dd6bd9c2d50d4319d3c3ef.png)
got some open ports...

![](attachment/73b02485249b25a889021f39965e4393.png)
Got versions by nmap aggressive scan...

![](attachment/d9c7c81ac036651c281359f25ab981c8.png)
cannot login to ftp using default creds. let's see if this version of ftp has some vulnerabilities or not...

![](attachment/db70ceee4886ba27ce235a464913f4bb.png)
So the version running is 2.3.4 and contains backdoor command execution vulnerability and the exploit is on Metasploit...

![](attachment/6b7972dd57a38fd90312db8c8ae9fb57.png)
got the exploit, let's set options and run it.

![](attachment/236a17d148905618d88e540bd2964024.png)
oops, it connected but then gave an error. But it was trying to connect on port 6200 which didn't come in the scan, that's unusual. It was connected to the backdoor but there was no shell...

Let's do a versioning scan on port 6200.

![](attachment/20b3b2c082bca7bcaf827d7161993ba0.png)
The scan gave a lot of php stuff and the name of a shel "psy" running 7.2.10 version of php, wait does that mean it is running php shell. let's search for "psy shell php".

![](attachment/0c144dcf48db312097a4668a01463bd8.png)
So it is a developer runtime for php and an interactive debugger in php. Let's try to connect to it using nc...

![](attachment/c8126e7bd7c927bf43dac4cb50e6e4f4.png)
we connected to the php shell...

![](attachment/5a00d028cd089d4c56284dda1e7e5b3c.png)
help command gave us a lot of commands we can use...

![](attachment/eecb3aed9f5e351dda41761930f0ef70.png)
Will be using this function to see more about the php running in the shell...

![](attachment/00511eb879dab3723e494862307b7322.png)
So after the above function got this which means we are logged in as user "dali" and the server running is in user's home directory.

![](attachment/765c850a890977643020377c80fc8b24.png)
cannot execute functions like "exec" for safety reasons probably.

![](attachment/7e203b3a2ae389f3bcd7a4797da1fa0d.png)
then came across this function...

let's use it...

![](attachment/87b54a4f65163bb8090186923223f7cf.png)
wooh!!! we can see directories at least...

![](attachment/0a03b2be3de1a36925835fa9761c722e.png)
Got some users..... in /home directory. Our php shell is running as user "dali" so checking "dali" user's home directory should be priority.

![](attachment/20152fd300fe8953ef2b1124727742a3.png)
Got some directories and files.

![](attachment/b712c7b0b21c51753717c3bdbed8bc7b.png)
we can also see .ssh directory although don't feel relevant in this case. Rest files and directories were of no use in dali's home directory.

![](attachment/e7203940c14be05355cdbef340aa1c77.png)
in user "berlin" home directory found user.txt, our first flag, let's try to read it...

![](attachment/24c2c82c1f5504d8ca345ce89b93175d.png)
will be using this functions to read the contents of the file and display it.

![](attachment/ab0a5cfbe2752634eb8ffbdd13621c01.png)
Permission Denied!!! But at least we were able to find the function to get and display the contents of the file.

![](attachment/fe60dc9b30b68d34e37d96199752ccaa.png)
Found a "ca.key" file in user "nairobi" home directory, let's see if we can view it or not.

![](attachment/b23a47f7c7a4bbb417f1be2b6be49782.png)
Got a CA private key.

![](attachment/a1d05675f75dda93a43117b1d695c6c5.png)
saved it in a file name ca.key.

In rest user's home directories didn't find anything interesting...

Let's see website now...

![](attachment/da00d162f530184e6ca227f4fee5ac61.png)
So this the website running with HTTP.

![](attachment/cc083f4f1863a774e645357c2d001a31.png)
This is the website running with HTTPS and it says that we require client certificate to actually access the website.

Now this means we need a client certificate and signed ca certificate for an ssl (HTTPS) communication with the website.
Let's do it using openssl then...

![](attachment/0ccf89c547bc898f8a75f9d137bd66c8.png)
So "genrsa" means generating a client key in rsa format which will 4096 bit in size.

![](attachment/3a924c08a3eeae26bc774596a17c5e4a.png)
So this command will create a signing request using the client key generated.

![](attachment/8c9e5dcb0144817ef8b6c1f048f3e9a9.png)
Download the website certificate from the https site of the website and renamed it ca.crt and self signed the certificate request and got the client certificate.

![](attachment/61b3acfba2639bee6cc613a67d6060ae.png)
converted the certificate into p12 format so that we can add it into the browser for ssl.

![](attachment/2284130ce3b1af0d96b225064fffa08a.png)
Now let's add the generate CA and client certificate into our browser...

![](attachment/6354c69c0d76e89531bc06d07af5600a.png)
So import client.p12 in "Your certificates" section.

![](attachment/4ef86aa1c156419277e6ae48660b2cb5.png)
in Authorities section add "ca.crt" of the certification authority.

![](attachment/a0a97a0f5833e5816650b991873261e6.png)
after adding the certificates this will come....

![](attachment/7ae2dca2f9568bb453055c4194ddfdf6.png)
In this image we can see two things, first the name of these files are in base64 probably and second the url as "path" query parameter which means there is a chance for LFI.

![](attachment/25312c511148e0ddd38d60354e48a241.png)
Was write file names are in base64....

![](attachment/2e3481a654f31926520011d3f3dffdaa.png)
so changed the value of the path query parameter to ".." and it showed directories... Let's try to grab private ssh key to get more hold of the web server.

![](attachment/ebe53f7d9a7b4b4a66895e4246f95620.png)
cannot click on id_rsa.... But file names are encoded in base64 and i noticed that when any video or something is being downloaded whether from "SEASON-1" or "SEASON-2" it is from a directory named file...

![](attachment/194ca3107911370946f80cc03f20e26d.png)![](attachment/e87dd0cc50b51c8605ce4e29cbba4ef8.png)
so encoded the path of private key in base64 and then it automatically downloaded the private key.

Let's try to login through ssh now...

![](attachment/81f65546b548783016328ac47e264172.png)
So now tried to login through ssh with various possible users in the system and professor was right...

![](attachment/a18602f0e959b27ceea74068fbed2e2a.png)
didn't find anything worth it in user's home directory apart from some .js files.

Let's run pspy and linpeas for further enumeration.

![](attachment/1363328667024620649b8478eee1f4a9.png)
Found a cron job running node and a .js file in home directory of the professor... Let's see what is it....

![](attachment/c2fb71763b9b139792c630f71fd5091c.png)
memcached.js was not readable for professor but found this command in memcached.ini file.

![](attachment/7f2c4cb25801ee9c240bf2ced95a9c89.png)
So changed the name to ini.bak and it will not change the permissions but the inode mapping.

![](attachment/5e178d68555d1afc44541001fcee0d43.png)
created a .sh file in /tmp directory in above payload to get reverse shell...

![](attachment/f574e3e8c8c35467bdbf6299421245a6.png)
created another memcached.ini file in the home directory and when the cron job will run it will run the payload in memcached.ini file as root as it is a cron job and it will execute the shell script that we created in the /tmp directory and then the payload in it will give us a reverse shell as the root user.

![](attachment/3823f8107c230542e87626cb02c2bd53.png)
got it!!!

![](attachment/1d8b443d1db804e367e138cf21995e54.png)
So was confused with ini and node js and there relation so searched it and learned that .ini file consists of the configurations with key value pairs, so here memcached.ini was the configuration file for the memcached.js which has the command for the cron job for memcached.js so we were able to know what was happening with the memcached.js even though we were not able to access it.

![](attachment/baa51797553fbeb0653fdf2d1bccd5e5.png)
So, got user flag in the home directory of the user named "berlin".

![](attachment/0c4a29dbdf36b9e7729d0e248860214f.png)
Got the root flag as well.