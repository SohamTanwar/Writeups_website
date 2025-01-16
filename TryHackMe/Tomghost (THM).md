**ip of the machine :- 10.10.142.34**

![](attachment/d8b361e299fb5630806134cf6f45d958.png)
machine is on!!!

![](attachment/375263cd7082512398789bc2d0a2b8bd.png)
got some open ports.

![](attachment/999598ace394cc32c39ad3498d93c30d.png)
Did an aggressive scan and found an apache web server an port 8080.

![](attachment/b67fb076214adea2635a093e89245bdc.png)
Now let's start directory fuzzing using ffuf.

![](attachment/a8971732a91ff83e1ab6797aafefe323.png)
Found some directories. Let's view them manually.. So didn't find anything in the directories which was pleasing except the version of tomcat which was "9.0.30".

![](attachment/5c98ea8c5b66d726a9c61873ecc794ea.png)
I searched apache tomcat 9.0.30 exploits and it gave an exploit of metasploit.

![](attachment/2e44b3ac36264b7e59d9e8c7dcd564cb.png)
So after more digging came to know that this was based on a CVE where we can manipulate apache jserv protocol which basically pre-configured with apache tomcat 9.0.30 and AJP is running on port 8009 so let's use the exploit and see what happens.

![](attachment/62cee5db2af504c40275b8355e748e8e.png)
So after setting all the options, we run the exploit.

![](attachment/62d96a7a81ece6074a4a328b2fc17a73.png)
Got some creds. May be for ssh...

![](attachment/948f5d4c9a2ff063af669e5b7cfa1beb.png)
was right, for ssh for user "skyfuck".

![](attachment/9137fbcfb7b3cca10b8b7078bf5f2c5b.png)
there are many interesting files in users home directory. Let's see them manually.

![](attachment/fa1fb1e42290c735f4c6aa5fffab49ed.png)
in tryhackme.asc file found a private key. That's strange!!!

![](attachment/4c7ea0af2da7bf722a0f5c32982d928a.png)
credential.pgp file. But looks a bit distorted. So let's search what the hell .pgp is.

![](attachment/55d8982d693305d6f5051f149c83c56a.png)
to crack pgp (which is used to encrypt creds.) we need a passphrase and a PGP private key. We have a private key and .pgp file. Let's look for the passphrase.

![](attachment/c9fdbe23274a18f603ae0a8e10bf8037.png)
came around this. Might be helpful!!!

![](attachment/c5d63d6b9d20122a5332bdfdb9f31cb9.png)
First transferred the hash of the private gpg key to hash.txt file.

![](attachment/f590504b73d42e59757df771250bcc40.png)
then cracked the private key passphrase ("alexandru")

![](attachment/780f65624cb235dacadd0f17f36573b3.png)
So used this tool known as PGPTool for this purpose, here you have to add your private key, then add the encrypted file (.pgp) and then after entering passphrase you will get the decrypted content in a file.

![](attachment/69b98fd81c35ab193a164aca21699a06.png)
So got another creds.

![](attachment/fdc98e43f324327a834e5fc6a272fb4d.png)
Before logging as another user, also searched if user skyfuck can run anything as sudo and was unsuccessful.

![](attachment/5a0532da6c6c869082e4d1bbddc067ad.png)
logged in as another user now, thus performed horizontal priv esc.

![](attachment/d5f20916e985db44fde96ae62a22e5a8.png)
found first flag.

![](attachment/7c356ff67f7792e75be774f3a13e0ef0.png)
merlin can run /usr/bin/zip as sudo with no pass. Let's go to GTFObins.

![](attachment/262b370af15e4c41cc8dedfa00bdd41e.png)
So following this way to get root/pwned shell.

![](attachment/9b905a3714137f62603601e1302bbe6b.png)
yay!!! got it!!!

![](attachment/fd1a472658ae51b313cc831e8e5fb3f1.png)
also got last flag!!!
