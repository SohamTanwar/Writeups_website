**ip of the machine :- 10.10.34.117**

![](attachment/443a7cd37b9e2df77c33d6eee8f126de.png)
machine is on!!!

![](attachment/f90ecc2d5a5d9d2cf4ee6effe89c3dad.png)
found some open ports!!!

![](attachment/417de4e5df615517dc1838aa560aaad3.png)
So found the versions of the services running on these ports.

![](attachment/9a80c7ae6dbeca551b39d00aeee4bfaa.png)
Did directory fuzzing using gobuster and found decent results.

Further will be fuzzing /assets/ directory.
![](attachment/341d83773d433856a99e416e1028555a.png)
found some more. Also did a Common php file name scan because it doesn't show php files.

![](attachment/914f8f13e84295843e4034deba883020.png)
Told ya!!! Found one!!!!

![](attachment/a77bfe7c8e93771a180c6997deef9881.png)
/images we cannot access.

![](attachment/0d69df2170645f1219cf1a3c281b604c.png)
So was not able to find anything as such in the machine for rev shell, so out of curiosity asked "leo" about possible php vulnerabilities, and command injection is what we can try at least by modifying the parameters and query in the language.

![](attachment/fe725c9080cdf3dcbbbb724ae0c96a28.png)
So i added a query cmd with "whoami" command and got this gibberish stuff which said www-data and we also found a place to add revshell to.

![](attachment/94814e5b297797135062c052117cca47.png)
Bash payload was not working so tried adding python payload which is the second most common for revshell after bash and surprisingly it worked.

![](attachment/b8560dfafb40ba1714db8251f98bc21b.png)
So in a directory named hidden content, found a file and a passphrase in it. Definitely base64 encoded.

![](attachment/e55f007f3bcef01e4c9257605a399c64.png)
Okay!!! now let's see where to use it!!!!

![](attachment/6a52ce150b42d5a697e9a69ae1519d94.png)
found possible usernames.

We got two images which we downloaded. Now it said passphrase and not password, so maybe it is the passphrase to protect steganography. So let's use steghide for it.
![](attachment/13179ef17ed9885294b0dffea6c29e0b.png)
It is showing file format not supported let's see hexdump to see what's the problem.

![](attachment/bff0b272dadf6ef33faa9c76ec4e97e6.png)
it has a PNG file signature so converted to .png but still it showed the same error. So earlier the file was in jpg, so let's change the hexadecimal values of hexdump to match jpg.

![](attachment/571bde57091d303be903ff2653666dad.png)
also used file command btw and it showed data, which means something is in there.

![](attachment/37e6c52db34748abdc90a0185faf1a59.png)
so changed in in hexed.it

![](attachment/9217f76af29289834f48f35f364847aa.png)
got a file!!!

![](attachment/c1feeaeebecf8d9192e19ec013541b65.png)
Got creds of the user "deku".

![](attachment/3b3c51a5f3e1142ce8b9c488f33c539c.png)
was able to login as deku!!!

![](attachment/a91224562c2e26c28ccb61bbd010400f.png)
got first flag.

![](attachment/f5bb9e731a337777a208b228c4a2399a.png)
found a script in /opt directory.

Now after understanding the script's source code, 
![](attachment/d57fcb28026dbb3c9bd378d380a6f93e.png)
generate a ssh key in local system not victim's machine.

![](attachment/9bd1175f176a2d5515040eeb37aefab7.png)
after running the script as sudo as user deku can only run that, it said feedback saved. SO saved this public key generated to /root/.ssh/authorized_keys file.

![](attachment/444d331eb8faa5f8824c1ad1c9e29927.png)
Then we can login using the private key to directly get root privileges.

![](attachment/de2b8092a8f5b48d8888605b0e64f764.png)
we got final flag.....