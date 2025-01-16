**ip of the machine :- 10.10.151.68**

![](attachment/f92dc78b176862d85741cc017c20af00.png)
machine is on!!!

![](attachment/c9947c4af2694f599f7cd8161500f59d.png)
got some open ports..

![](attachment/3ed76ca172ddbc14c29828e7cafe7dbb.png)
not very pleasing.. Let's enumerate web application using ffuf and manually afterwards.

![](attachment/cd1142536871b3a26f781c4b285215ce.png)
only got one directory worth enumerating manually.

![](attachment/3e0ef53f78872917d303167ba9b66e47.png)
apache2 and that to in ubuntu huh!!!!

![](attachment/ec49b82e8c05ec86882c01fdf2c6b9e6.png)
Got to know about SweetRice CMS. Let's look for any possible exploits. There were many exploits, but didn't know what to use so instead further did directory fuzzing in /content/ directory.

![](attachment/2f4850b1e2924eec23e5d83a57402181.png)
got some directories, let's look in them further.

![](attachment/13c4a546e5087983ca939e9066bbe7cf.png)
found this in _themes directory.

![](attachment/5a76b1ec15c934827a08a0f43548944c.png)
images directory.

![](attachment/dcd124a418e175fec541d4efe332b73a.png)
inc directory.

![](attachment/9fc84d79365b8f0705a65738c24dcdef.png)
js directory.

![](attachment/7664644b6b615f816d999434eb8b999b.png)
found a login page.....

![](attachment/d991dec720ed431487444883c46f7811.png)
in /inc was able to download a file so went for it.

![](attachment/7410dc334de526aba3be89dec6d6634f.png)
found a hash in the file.

![](attachment/ef9eef144914490c15457d82db1010d9.png)
cracked it. (Password123)

![](attachment/156df211c2cb55003787e4a90466c181.png)
was able to login with creds. manager:Password123

![](attachment/18728cff11a5a3aa9154619ff0984aa3.png)
also got it's version. Let's search for any exploits now.

![](attachment/017bd7868da531cf2bfc8ffe5886f112.png)
found 5 exploits, but will be using 2nd one.

![](attachment/d4bede40252c98f5b88a0d6a8451a0fb.png)
go to media center section and upload the php revshell but zip and then click on extract zip archive as it will extract and then execute it.

![](attachment/d9302f13e1cf72a814499971b6838d22.png)
Now click on the file uploaded with the random name.

![](attachment/55de88de8898019612d225b519da2ae8.png)
Got revshell.

![](attachment/b77cc2d7ba041290c0f69b53ba000f57.png)
So went to /home directory found a username and also got first flag.

![](attachment/5f921b4d0b67e95a6175626de2e02693.png)
Also got some creds. for mysql as well. Let's try them.

![](attachment/cb3c17defa1607ae4aef5e9e58ecec0a.png)
got it!!!

![](attachment/6abc71a8e54b84d7622ed535485be5c9.png)
got password hash for rice....

![](attachment/fa20a2eecb5402f44b9034b725709e28.png)
password is same as mysql. 

What if rice user is the itguy user in home directory?? Let's try!!

![](attachment/cf791d1ec0a93d7240566a56f0246043.png)
nah!!! was wrong!!!

![](attachment/e6c9589229d33f6ad979ad6ee675af6d.png)
so there was another file known as backup.pl and when viewed it, it is indicating to a script known as copy.sh in /etc directory.

![](attachment/d0889f1a94e2bcc96b6ba88d9cebb89d.png)
so as another user saw what permissions i have for this script and found that i have all permissions other so let's try to add a pwned/root shell and copy.sh can be run as root so now problem.

![](attachment/a59f113f6a4220265a520f3ab0bcd3f5.png)
did sudo -l to see what permissions i have as others and saw that i can run only one command even as sudo with no password.

![](attachment/0cc15bb3e12759be41f18911bef12194.png)
added "/bin/bash -ip" in it so whenever i run the privileged command it will run bash in privileged mode.

![](attachment/caea391a1e5bc22b57972350c14dc0ab.png)
so after running the command as sudo, i got pwned/root shell and got root flag.