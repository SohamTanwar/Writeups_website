**ip of the machine :- 10.10.59.210**

![](attachment/db73baa44aff274ed5c14417e84060b4.png)
Got three open ports...

![](attachment/fd0c2f0bc6938f7fbaa5c819ab87e6e9.png)
Did an aggressive scan on the ports and found out that anonymous login is allowed on ftp.

![](attachment/82af29841aa8c7ff62c71b4d0cf12d2b.png)
Found a file, let's get it.

![](attachment/0faab10bf7066d1a9bfece6b42243d98.png)
Got it, let's view it!!!

![](attachment/96b3bd9f195a520041db68ce508ecbb2.png)
Huh!!! what is it??

![](attachment/bf8ac1e303abcc329e3c663d0723f105.png)
It was a base64 but still the text that we have got is strange!!!

So, didn't find any clue... Let's see the web application then...

![](attachment/339398766055b099e13e0d53755a9a1f.png)
Nicholas Cage themed web page and found nothing in the src. code. Let's do directory fuzzing then!!!

![](attachment/8f950484765940dbc9e6cd78d50e1d83.png)
Found two interesting directories, scripts and contacts, let's view them.

![](attachment/ce0d31073f685136f01131b6bffc9f0b.png)
Uh!!! Found some!!!

None of the scripts were useful, these are just random conversations between different users that doesn't even make any sense.

![](attachment/a5d90a095d12b14df0cf94f9ef479c20.png)
In contracts directory found something with nothing in it.

So after finding nothing in the directories, went to dcode and boxentriq cipher identifier and analyzer.

![](attachment/6045ebfde402eb24879ccc90e82e3995.png)
![](attachment/036979fe90543f44afd147e2549a2cd4.png)
Both were suggesting that it is vignere cipher.

![](attachment/cbe60b19303360a2e913671346d3d7fb.png)
So vignere cipher decoder of dcode and boxentriq was not working because both of them were asking for the key and brute force was not working so searched and found a website.

![](attachment/3587debf3b57ae469c560a30f1f5121b.png)
Got some text.

![](attachment/5fbf8917de3ce3911ec5c50638384330.png)
Got a password.

![](attachment/36615e431c42c90c9ee32bc5da09ea0f.png)
So username is weston. Now let's login through ssh.

![](attachment/b11f6140e51c0c624b3011ba90892866.png)
Logged is as the user weston.

![](attachment/4a1147edfeebaa646c31f71a0ff163b8.png)
Found nothing in weston's home directory but also found another user named "cage".

![](attachment/bd0348b5b3c0272276f0d99e252f677c.png)
We don't have the permission to enter user "cage" home directory.

![](attachment/97734b635a7d797ff521da68de8a597c.png)
Did "sudo -l" to see if user "weston" can run anything as root or not and it can "/usr/bin/bees".

![](attachment/dd7f4504c3021264dd64a403774d783d.png)
So no command/binary with name bees, so it is a custom binary/script. Let's see it.

![](attachment/ecb309cf4ddbbf5447010d74c0dffd5e.png)
Nothing as such...

![](attachment/4fce47b2b8d3d57df8728d2daac44bfb.png)
We can run it, but we don't have any permissions to write to it. Let's find any other way because i think it is just given to maybe confuse us.

![](attachment/97019ce1a2d12678c17788b2f8f627a7.png)
When i entered /opt directory because i found something, it ran a script, so maybe a cron job is also running which is also exploitable.

![](attachment/78eec2bbc06906775cc8244b69033acb.png)
So, in the directory found a python script and it is fetching records from another file which is also hidden and then basically executing a system command or simply printing the quotes.

![](attachment/299f84a8192bca65311460bf1ed077a3.png)
Found it, so it is fetching quotes from this file.

![](attachment/a39ba91a5317adb66ea833ce83697ba7.png)
We can only read and execute the script but we cannot do priv. esc with it but if we are user "cage" we can do it...

![](attachment/4d00de5b892ce871eb08f650e8afed84.png)
So went to /var/www/html and found another directory which was not present duing directory fuzzing and it had a .mp3 file.

![](attachment/3e8c575437496256ebb1dfbc8f781ad3.png)
So got the file in my machine for further analysis and found nothing in the mp3 file.

![](attachment/5ff0ce83e63411153c1145ac74a1e444.png)
So, after finding other stuff, though that if we cannot edit the script which is fetching from a file ".quotes" but if we can edit the .quotes file, or basically if we can add a reverse shell in the .quotes file from which it is fetching the quotes, we can become user "cage".

![](attachment/025fdc5c5491046b11a297ef6a18beb6.png)
So, removed all the quotes and added the reverse shell payload and now let's wait for the cron job to run.

![](attachment/2a78aa430642320cbdab00badd5a43b5.png)
Let's see if the cron job is even running or not because after adding the payload, didn't get the reverse shell.

