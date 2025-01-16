**ip of the machine :- 10.129.231.58**

![](attachment/f852b3d833793336d61e575fb51bfe4e.png)
machine is on!!!

![](attachment/7505b58c2ff8211f9e1e2f1e4d649fe0.png)
Got two open ports!!!

![](attachment/5ce3076a1e78a74ee36d1032373ba622.png)
Got version of the services running on the respective open ports...

![](attachment/5a255ed5057c6c23cf595e2dcadd4f49.png)
Website looks fine and doesn't has any link or something and as well as directory fuzzing is not even working...

![](attachment/74eb149d38378d4dc616b27ee3ce4ea3.png)
Then searched the web server running on http with it's version as it seemed different and got an exploit, so will be using metasploit for this one!!!

![](attachment/a6c00a5e96d7d88621bc9f1414f278f5.png)
So after setting all the options, i ran the exploit and it worked, session created.

![](attachment/3a624ae11bf3e516613906a6c1351379.png)
There is one user's home directory but cannot access it.

![](attachment/59c5e3cbd31059320f0eec5cd35d7b3f.png)
So went to /var directory where there are all the files and directories for the web application running on the web server.

![](attachment/f6a313cf015988badbd4b8c4e3fac771.png)
got some interesting file in conf directory. Let's see view them...

![](attachment/3268dab9d3ec9ce4816a059c367b82a1.png)
maybe we should look in htdocs directory after seeing all the files here...

![](attachment/fb2248bf8ddfb4ee4f5e2aa0f44264c8.png)
Oh!!! password hash for user david, we were looking for...

![](attachment/70bd9a4ed387bba64131b5d0ce8a9f82.png)
cracked it!!!

![](attachment/951607e8ba4c253cf5e541a84f59a2fc.png)
Now that's strange!!! It didn't work!!! Let's go to htdocs directory which was in conf file for more information...

![](attachment/e711d80b7c079b20a860d9d0c64b10e9.png)
Nah!!! got nothing interesting, just the src. code of the website...

So, found just a password and that is also not working, let's try to find some more stuff.....

![](attachment/3b8bceebe344a9d30a76fe36bf9ad698.png)
I overlooked the .conf file, it contains a directory.

![](attachment/4443cc9ed12f2c65b2ca1c208dd5700d.png)
i cannot cd into /home/david but can into /home/david/public_www as it is a public directory and have permissions to read and access it...

![](attachment/04e944ca867ba35ca8f3547b89105a42.png)
here, got another directory and found a .tgz file which looks interesting, so let's get it back into my system...

![](attachment/45b0abbd6df701bdddfcebefdf88dfd9.png)
So first started a nc listner with output redirecting to a file we want to recieve from the sender.

![](attachment/51e22d0062773dfdfef43a33a96de27b.png)
Then send it to the reciver with ip and port specified and file we want to send.

![](attachment/b14b857af7368b31380b968ce6dad1c1.png)
file recieved.

![](attachment/0754df746175798fa124db09ad71c2b4.png)
Extraction revealed a lot of files...

![](attachment/18838a43c0f7ff964cf4ad7083b73769.png)
Got a private ssh key in order to login as user david...

![](attachment/2ded054bd2ae32318722a7312069c9b9.png)
It is asking for the passphrase, let's try entering the password we got previously.

![](attachment/80dca86ce99352dfe9faaeec034959b9.png)
OK!!! So it is the wrong password!!!

Let's find the passphrase using ssh2john.

![](attachment/7cdf815fb0e62dc77ee722fe79e75f57.png)
created the hash of the private key...

![](attachment/7ade76e21d43212d9fec85cecde98ff1.png)
found it!!!

![](attachment/7b6f20bf3111d70c83964dd10bb926bd.png)
Got user flag...

![](attachment/1da7011f0e65c35fe1cabb7c0f59b6d4.png)
OK!!! cannot see what user david can run...

But also found a bin directory in user david's home directory, let's see what is it.

![](attachment/fa28c3ba0a516634c586405c1ed36e16.png)
A script only david can rwx and no other can.

![](attachment/ca9a869533de70627fc12be840d6e478.png)
saw the last line of the script and found out that user david can run journalctl as root user, so let's modify the script and exploit it in order to escalate privileges vertically.

![](attachment/19618fd27b665c7a73487e361367d786.png)
Got the payload in order to get shell as root user, let's see how to use it!!!

![](attachment/ed7df6fee9832b7e65e7ec639abf0184.png)
Just ran the script, and found nothing to inject the payload. So now, let's edit the script then.

Cannot edit the script using any text editor!!!

So let's use the command directly.....

![](attachment/182d99d07296609d186259c685766d09.png)
So directly ran the command and it invoked less to show info. but as the root user. Let's add the payload then...

![](attachment/f400344c425aed90ed0c71280fa9951c.png)
added payload and escalated privileges...

![](attachment/f843c69958b7107ea8f2faf10c12599f.png)
Found the root flag...