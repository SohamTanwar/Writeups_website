**ip of the machine :- 10.10.11.37**

![](attachment/6ff56fa473cb446f002d6f7856fbd913.png)
machine is on!!!

![](attachment/17e006363f8f2ec4326e8e920ae02165.png)
Got two open ports!!! 

![](attachment/9b04eec52a32f0d8f8bb1304066d3654.png)
Performed an aggressive scan on the open ports and got versions of the services.

![](attachment/9bbadc680e12aee1621b1637966efa44.png)
No directories as such. Let's open the web application and enumerate manually.

![](attachment/5600b9df9c8d0b9e1893e24c05f6e768.png)
Found a download, let's see what are we downloading.

![](attachment/3fcc4cef855e7630161bc3a550ab323f.png)
It's a .apk file. Let's decompile it and see what we can find.

![](attachment/11a853131111870f727eab877d02e5e0.png)
Used jadx to decompile the application.

![](attachment/0e095d8d6b1cb92bae856fe7753368f5.png)
Used "grep" command to view in the file for the domain "instant.htb" and found two sub domains and an api key which is used for authorization on a specific sub domain.

![](attachment/874a8f77397ce8a20527f85dc5fae821.png)
Added domains in /etc/hosts file.

![](attachment/49927e344df7410dc4eb79cf4368d872.png)
1 showed 404.

![](attachment/ddf0f64181e9f269cc256497e3bfdcec.png)
Other was for the api one. Basically we can view api endpoints and see what to get from those endpoints and stuff.

![](attachment/a055dc61cff3e2cea38b3744d8c24363.png)
We have to authorize with our api key to see the endpoints and did that.

![](attachment/1ccaa3c1dc29febc6d573ad90eda566b.png)
So, on one api endpoint we can view application logs of the admin.

![](attachment/9f712284f030d6a082ffd9618e70541c.png)
SO, found this api endpoint where we have to query with the file name and we can view it.

![](attachment/9e3432a65106b6478182b9e770b19102.png)
So, used burpsuite to test whether we can exploit api endpoint and was able to view /etc/passwd.

![](attachment/a03d6789d668619979762b84e1ae8a8f.png)
So, found a user and attempted to view it's ssh private key and got it.

![](attachment/5c7c73db4f9dd01da140842d002410da.png)
Logged in through ssh and got user flag.

![](attachment/b7baab182965e627b472a8be329c86cb.png)
in /opt directory found a backups directory.

![](attachment/f39ee28609a6d9305b66b2c75b8c10cd.png)
Found a .dat file.

![](attachment/44b274280a08a553792a0f4d91fa5a94.png)
So, found this tool on github and let's try it.

![](attachment/722da43efa1780d1935505df61bbbf8f.png)
So, used the tool and found the password of the root user.

![](attachment/4adefc43263aff4b5c8895f5a22454b0.png)
Got root flag.