**ip of the machine :- 192.168.122.194**

![](attachment/55d7bb8054fe26b5144d0f0e61c044a9.png)
machine is on!!!

![](attachment/39b8bda5f5050283595c53390c70a53d.png)
Got some open ports.

![](attachment/3580d967e123dc04b73199d54ef92250.png)
So, found smb, found http running on port 10000 and 20000 and nothing much interesting going on.

![](attachment/5cf5e1065c2e679844173a6f1cdbe0ec.png)
Just the default page.

![](attachment/688ee9a747da13042293b0a94de1588d.png)
In src. code found some encrypted stuff. Seems like brainfuck to me.

![](attachment/4f67179b7d423394ec79b34629771d01.png)
Seems like a password to me.

![](attachment/fc96de983f6f4fe5f39ea996355eaffc.png)
Used enum4linux and found a possible user name "cyber".

![](attachment/fada52fcd13d8098df7838c9622af76b.png)
At port 10000 found a login page, let's enter these creds. here.

So, port 20000 is also running webmin, on that it worked but on port 10000 creds. didn't work.

![](attachment/c510251c76f1bdf3ee3135647bed21fc.png)
Found a command line panel after logging. 

![](attachment/ac3c25bfbe060cb02f1a86b111c55209.png)
So, added our reverse shell payload.

![](attachment/b970add1393977f1cec72f65f52a2cfb.png)
got it!!!

![](attachment/67d3648cbecee23ae780283f6d59e0aa.png)
got user flag...

![](attachment/ee6fda29cf930135cc9067b29ef94220.png)
Found a tar binary in user's home directory.

![](attachment/b889876b75da95dda31345ecca2b0331.png)
We can read the backups directory which is usually not allowed as it might contain some password. Doing this because found no SUID binaries or users.

![](attachment/042f21d8d0ced996191603fe58d8f073.png)
Found a file but cannot read it. Let's use tar then.

![](attachment/d0144d7c939160bbc5bea5d5376d45a2.png)
So, we can run tar and compressed the file with tar and then decompressed it and now can access the file as our user.

![](attachment/9b702f99f530676972464813b7b59088.png)
Got root's password.

![](attachment/2a0ec6abaa09ae0210361e4f09afb583.png)
Got it!!!