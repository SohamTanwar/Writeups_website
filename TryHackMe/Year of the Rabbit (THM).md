**ip of the machine :- 10.10.196.3**

![](attachment/89c2f202ff2a2523290b5885a0a950f8.png)
machine is on!!!

![](attachment/e2d6d8f80750e0e0e92fea3bfc96e049.png)
Got three open ports...

![](attachment/6e40a2e23646290eab4f9a5bce660956.png)
Found version of the services running on the open ports.

![](attachment/2cb9f49f740f6e5fdeae89c4bb9c8e7c.png)
anonymous login not allowed!!!

![](attachment/c8337dfd5972851b84d59db48c6e8cf9.png)
got some directories after scanning.

Also looked at the src. code after inspecting and didn't find anything. We can only look on one directory which is /assets directory.

![](attachment/7261fe1771930f54145c0d885138f193.png)
found two files...

![](attachment/f771223b978aeb6281ec44d148031f34.png)
rick rolled'

![](attachment/0b0e2b45c5bdeacc1605b33f6b2894ed.png)
in style.css file saw these two commented lines. Let's look at this above mentioned page.

![](attachment/5d6c3fa1312b980513bd877cfff8d068.png)
it is showing us this...

![](attachment/bb293933cf964cc7b6a1cd0c2addb4ad.png)
after clicking ok, we are redirected on youtube and got rick rolled...

![](attachment/e5d6466e4b1624bbc9fb563545a83e22.png)
So i used script blocker to block js on the web page and this was coming.

So i was being confused what to do next, so went to burp suite and start visiting website again and again till i get something interesting and in one of them saw something,
![](attachment/f1a4703414f2e17a8461076d13726243.png)
a hidden directory!!! and that to a get request...

![](attachment/545095a4ef32f3dfb73e21da8692bef2.png)
so went to the hidden directory and found an image...

![](attachment/c73dfa6a7f0367b3d751aab123f471f6.png)
So downloaded image and started binwalk but didn't found anything then did strings.

![](attachment/bb5931ca1ff77a4e7a2cbcf073f3cb42.png)
got possible user "ftpuser" and now we have to brute force the password.

![](attachment/b98fd7bdb1c445706a98a10167f0502b.png)
So created a password list of all possible password combinations.

![](attachment/61e9f6361dab6e1762a1b067eefef87c.png)
cracked it!!!

So pass of ftpuser is "5iez1wGXKfPKQ"

![](attachment/c1b35ed709e1c8fb48c5c13fcff9c6ea.png)
Finally logged in!!!

![](attachment/54d47696ff35737f12a1a10f418ebd9c.png)
Oohh!!! creds....

![](attachment/1246ef57dea14238a3f0ea5d96f6a3fd.png)
Got creds. but it's a bit gibberish though!!!

![](attachment/e5a031b45292d6120543eca5f2ea82bb.png)
So i asked chatgpt which language it is, and it said brainfuck.

![](attachment/ae528453cb8c20bac07db7446e850904.png)
So simply went to an online Brainfuck compiler and executed the code and got our creds.
User: eli
Password: DSpDiM1wAEwid

![](attachment/33ac84cad6f236600f0895b10070fc9e.png)
entered as user eli and also got a message from someone and came to know about a hiding place, probably a hidden directory.

![](attachment/6231fe8600477f1e5bee01bb9d030560.png)
eli cannot run anything as sudo.\

![](attachment/69fdf4724d003f9decd9fe66fd204bdb.png)
there is also another user, let's try to perform horizontal priv. esc.

![](attachment/e0c6c370e07d3a01fb54cdd43a656308.png)
So another user has the first flag but cannot view it. Let's go and look at that secret directory "gwendoline" user was talkin' about.

![](attachment/801e94e08a24ffbdd80fe054054ea980.png)
Found it!!!

![](attachment/e92124ce82879cc42366b7ddec213ac8.png)
this s3cr3t directory has a hidden file. Let's see it.

![](attachment/7b9b853543f9136e0c24310a324414a2.png)
Hah!!! found password of "Gwendoline" user directly in a message so called secret text file. Let's go and get our first flag.

![](attachment/957100c64b7c3896f5657233a3ff2325.png)
Logged in as another user "gwendoline"...

![](attachment/bbcce7d5fcf04d8ffde344a7c4155e2e.png)
After getting the first flag, did "sudo -l" and saw that user we are logged in as only access to user.txt file and "vi" command.

So privilege escalation using vi and user.txt file was not working and it had (ALL, !root) and not (ALL, ALL) which as usual so searched about this change in sudoers file probably....
![](attachment/a2ed5eec52c7e2122a2f8263fbbebbfb.png)
So after entering the weird permissions directly on the browser it gave me an exploit of exploitdb.

![](attachment/ce5eb8c36f7236bbe138351fbe4f8981.png)
let's download it and try to use it. (CVE-2019-14287)

So this exploit didn't work so have to manually exploit by understanding the code.

![](attachment/748d8396c294243fdd286424adbe0a0d.png)
So in code there was an example, if any user cannot run /bin/bash then we can use exploit and then that command to actually bypass it and it is a vulnerability of sudo command.

![](attachment/9f1cde0ded877b01b8be46a5fec4e83b.png)
First write this command.

![](attachment/d01351905cf2fe9f7e3139085f929aac.png)
this is our previous flag file.

![](attachment/3f25f22624c7d1d19d2a078dd191dc11.png)
Now vi is running as root user and in order to get a root shell.

![](attachment/fba801d1f4d62335a8c02c2efa120a2a.png)
first type this and then press enter.

![](attachment/f7ec190b0d85f63df08778b34a496cdb.png)
Now enter this to envoke the shell.

![](attachment/480ae111b3e5ea8618217eaf92464173.png)
Thus, successfully escalated privileges and found our last flag.