**ip of the machine:- 192.168.122.236**

![](attachment/8496e495fd33eb44945450a80d52845d.png)
machine is on!!!

![](attachment/fdcabe4a5f42613b16bc956ec58dab53.png)
Got two open ports...

![](attachment/77f017d8f32d526656c3a0a29b7cec2c.png)
Aggressive scan revealed the version of the services as well as one disallowed entry in robots.txt.

![](attachment/780ab909f24db29ff580c72921692a7f.png)
oops nothing here.

![](attachment/2c0e638b4045f39425bac1f8c5c38ea2.png)
A message in src. code although.

![](attachment/94e98bcf6ba37d163c3d9510cb7822c8.png)
Got a secret directory, as followed a pattern of the hidden directories.

![](attachment/e3b14e1adee9fa14b04a2b15a6d7030c.png)
Got a possible username and a hint to where look for the private key.

![](attachment/86cba0dde71c25e260ce9b061c355d4c.png)
Did .FUZZ because it would be hidden and most probably starting with a dot.

![](attachment/afe7ff2b6bd16b03a169fb880cb2d990.png)
So, changed the wordlist and found something.

![](attachment/cb7e52a9abde5f6b8babdf13c933b34b.png)
It looks like some kind of cipher.

![](attachment/3cc1eedcba1ff4522954f1a2e6d474ec.png)
Dcode cipher identifier told that it is base58.

![](attachment/50d986ac9eae32f8f28102defdaefabd.png)
Got it!!!

So, user said that this key also has a passphrase, let's crack it using john.

![](attachment/b904620f0a0f31a94183f3edc39994b5.png)
Hash created. Let's crack it.

![](attachment/34ebc3ae4805730a3076f136fce5fb59.png)
Found the passphrase and btw used the password list named "fasttrack.txt" because when chose rockyou.txt, it didn't crack the password.

![](attachment/601ed701238bfd059456a90819e2ad6b.png)
logged in through ssh as the user.

![](attachment/1ba4560b4d66e1b23910c690083406e9.png)
got user flag.

![](attachment/29def5df8d12a444188e6da17c36d51a.png)
So, saw bash history file and saw "su root", so maybe user has some privileges of root user i guess.

![](attachment/6894f3421c363e01188f78fc35306011.png)
A file....

![](attachment/e78e0d342d1d89044d853ee1522839b4.png)
Oh!!! so we have to do horizontal priv. esc. first.

![](attachment/7352d14d9481cd3111daddd2cd29804b.png)
Saw permissions as well as the code in the file. It mentioned webbrowser module. Let's search for it in the system.

![](attachment/dfde84d7fceadb79df92a9345cf1fa1c.png)
So, found one...

![](attachment/6afb810d7ea28f10e5f3c7e0c13ac179.png)
Oh!!! We have got some permissions!!!

![](attachment/0e17093fffc38956492939fec4446916.png)
So, added a bash shell execution command in the definition of a function which will be called when we execute the file in arsene user's directory.

![](attachment/e04fb0ecbb5a09f2000ba31ddc2201f6.png)
Got a shell as arsene user. Let's go for root.

![](attachment/90640a22ad3970575364d645a4d924f3.png)
Saw note.txt in aresene user's home directory and saw the content and found nothing but it also talked about a secret file. What is it??

![](attachment/326818394f69b20d6aa9d112df5f717d.png)
Didn't find a file, so did "sudo -l" and can run pip as root user.

![](attachment/3add92e3053f5ef722e91aaf7ec5afa6.png)
So, saw the payload from GTFObins and got root.

![](attachment/bbd0db9a6ae9bea6b0f0b6f7e29f7b3f.png)
