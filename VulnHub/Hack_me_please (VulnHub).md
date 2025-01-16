**ip address of the machine : - 192.168.122.182

![](attachment/1b8f85450e80c1643b274c249682c6b2.png)
machine's up!!

![](attachment/10b32ad92ca2469806451370df9eca7a.png)
ports running.

![](attachment/f9a67ff20bcde7c8b059be6e7a597200.png)
versioning info. Now will be running gobuster and nikto first.

![](attachment/b7371fb381fd7c17f28518429d2ac629.png)
found this in jumbled stuff for port 33060.

![](attachment/810030555887103b9621183efbad8361.png)
just got some directories.

![](attachment/0cf7526d67b59345eb8c88298e448604.png)
Now we will enumerate the web manually.

![](attachment/2e82908dcca4dfca32459d3172ea1ae0.png)
found this main.js file.

![](attachment/8aee16c754e8494a276a8cd7751007da.png)
going to the url and found this login form.

![](attachment/319bb817c69f009c327995f8ab62c848.png)
went to seedDMS github repo and learned about the structure and got to know about settings.xml file.

![](attachment/07f31265f98d0a6a8f563818684b6650.png)
in settings to xml file got some creds.

![](attachment/abc70f489275f7b86a479320a48c914e.png)
was able to login with creds.

![](attachment/f111525f4c8bfb73fdb17f96e8d1d749.png)
got a possible username...

![](attachment/4f474ae8b83e61ca3b71f62cb49c802c.png)
got password hash for the admin.

![](attachment/3a892e2dd3aeb85e3e34afc50e782e87.png)
password hash is md5 and we can modify database so let's change password according to ourselves.

![](attachment/d98aede24fa50d7bffa2fed0537fb598.png)
so set the password to 'admin' and generated md5hash is then updated in the table and then we were able to login as the admin.

Now let's inspect the website to see where we can add the reverse shell.
![](attachment/4ccc4fc5be0cd3dd5b367b5a07e07266.png)
added file and now we will redirect to a url to gain a reverse shell.

![](attachment/5b0a3ab8ef505f66a00173544e09c9df.png)
we got creds. of the user mentioned.

![](attachment/43d13b9cda89fe1d304b0096ea4a62b7.png)
version of kernel (in case had to use kernel exploit for local priv esc)

![](attachment/9fab1b2124ab2ef2e253a017fd92750c.png)
so here we are login 

![](attachment/409a0e4eb5c95d31387f8282d9e33dd1.png)
thus escalated privileges, as "saket" user can run all commands so shifted to sudo.