**ip of the machine :- 10.129.107.139**

![](attachment/897a36446d374bbc30d89f3e65e89438.png)
machine is on!!!

![](attachment/af064d1b7d056d973e28086c0bec95de.png)
Only one port open and that to 80 (http), so no need of aggressive scan i guess....

![](attachment/0afb1d8df64f769de9d92083e1946d90.png)
Website looks good, let's see what is mentioned in the blog..

![](attachment/2dd2932f24b4f8f112830680f5e46cba.png)
So blog is about a web shell which is used for pentesting...

Let's do directory fuzzing then....
![](attachment/02cdfe0dd87d6c142078a5f642042dcf.png)
Found some directories, let's manually explore them.....

![](attachment/e13a2f10e87399dbe42b7ebbc0e00a42.png)
found a directory with two files, let's see them...

![](attachment/77e4a7238a455b130973080a993d996d.png)
So both the files are web shell, so now will try to get reverse shell first.....

![](attachment/8640b9c0633683d011c06528989382da.png)
So bash rev shell payloads are not working.....

Hmm... let's try python then...

![](attachment/49d214d00ce9e56dbd4ffddb15b33020.png)
Wooh!!! got it!!! bash didn't work so tried python, if python wouldn't have worked would have tried for any other language or any other way for rev. shell or would have continued with web shell.

![](attachment/5820b9604933944e619665d2e4ca399a.png)
in home directory found two users and in one user's directory found user flag....

![](attachment/9bb4b4a58335e1adfd8de6fd5dd1630b.png)
used sudo -l to see what permissions www-data user has.

![](attachment/28bf8ddabed5baef67161ddf94cfcaec.png)
So first got a bash shell as another user.

![](attachment/45b13e9a2fcb4dbe84bec4a27fca6039.png)
In root directory found a directory only "scriptmanager" user can read, write and execute.

![](attachment/8d8b435d5fe30bed1ea4fbf73fb5b00a.png)
Only one file can be edit by the user and one by the root...

![](attachment/80655bd9d6d33373d8766d60ef3cd6f6.png)
Still cannot do anythin'

Let's see if any cron job is running or not which can actually help us escalate privileges.

![](attachment/dc9d9d86ccdba0dae029fd202a584819.png)
Let's run pspy to see background processes.

![](attachment/2821d51dc3c9e43596805ca4c9bbc98c.png)
So, a cron job is running which will execute all the python scripts in the scripts directory, so if we add a python script with a reverse shell then what will happen????

![](attachment/63df8c6cfe98dbfbd97e21629459588d.png)
added this reverse shell in a .py file in /scripts directory and waiting for the cron job to execute while we wait with our nc listner.

![](attachment/c157ef6d80e8f4991183bd538cb6eac6.png)
got reverse shell..... as root.

![](attachment/ee1d3066563e28b9a3459e87497744b6.png)
Got our last flag.....