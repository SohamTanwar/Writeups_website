**ip of the machine :- 10.10.5.6**

![](attachment/45a1671ae1bb8b34f1f50d13d3cbe2bc.png)
machine is on!!!

![](attachment/81f724beff87b50b9a7816a5dbb2569a.png)
got 3 open ports.

![](attachment/e8c3e588576ab46ab63d1b8e94f266e7.png)
we can login to ftp server with username anonymous.

![](attachment/8b44b1d10082ad63cb0ec5a517954739.png)
logged in using anonymous:anonymous.

![](attachment/cf8f24ccb22c52ff206cdc9be7e893fe.png)
Found a file "note.txt" and downloaded from the server.

![](attachment/3977f545c4061022c8f86bb615503342.png)
Got two possible usernames "Anurodh" and "Apaar".

Let's do directory fuzzing using ffuf.
![](attachment/f21dd186856fa15160c1bc62e781911f.png)
Got some usual directories but "secret" looks interesting though.

![](attachment/d90388fc755faa87bda361e5cf8ed051.png)
oops; what is it!!!

![](attachment/550e9e68a35559ebecc125148103c792.png)
i typed "id" command and it showed this!!! which means it is like a web shell.

![](attachment/23a0c75f536945db82c6aff43cb43a10.png)
So after adding rev shell payload, it showed this and didn't get reverse shell. This means it is blocking some commands.

![](attachment/8359827471633c577cbb322e5c37efb0.png)
so right now id and find commands are working, ls,cat,cd, even bash not working.

![](attachment/d437c9b34a68d35ea5edf536a58b9404.png)
pwd is also working.

![](attachment/3169e452da2bc07e6a383cd4f505fce1.png)
So started a python server and tried to use commands like wget and curl to see if i can download something, and it worked. So let's think how to get rev shell now.

![](attachment/d393b463844647e1083ca37ae7802847.png)
Added python rev shell but with a random back slash in python and it worked..... Although it was a random thought though. Because it was blocking every type of payload for rev shell, so did something different and by chance got the shell, because it won't filter it.

![](attachment/e6662d9d0a362bb0e5ec13b3445af080.png)
Got it....

![](attachment/f17d2cfe6bab1ecb41d71c257ed730d2.png)
So in /files/account.php file, a sql query is given and is executed and is from sql tables named "user".

![](attachment/f3c3e8e2847a25657468d03202a0baaa.png)
hacker.php, "look in the dark and you will find your answer". I wonder what does this mean?

![](attachment/495248d2323bf1f55b75d517749bc9d6.png)
in mysql database. we can login as root and localhost and even password is given in index.php.
![](attachment/75191a5a8c4378f498bc278338337aa8.png)
So, was write this gibberish was the password for mysql database as root.

![](attachment/12feb7c6781df988392162eb54342f7f.png)
Got some password hashes.

![](attachment/6b05b9b3e9f305e02d559d1020c88cc1.png)
unable to crack of root, so will move another database, named webportal because in one of the .php file, we saw that it is being used for authentication in login form.

![](attachment/c677a3ead80f42499dc39827bf8039c7.png)
And it only has one table.

![](attachment/1edd030be955c223ca2bc6757d59fbaf.png)
got both the user's password hashes.

![](attachment/6bec3e47e7600404787040853686d482.png)
got password of "Anurodh", "masterpassword".

![](attachment/07c2406841f4c74ce7305c21141b8946.png)
Got password of "Apaar", "dontaskdonttell".

![](attachment/6307325b48036545b868f06777f5095e.png)
both the above users exist, let's do some password spraying to see if they are reusing password or not.

![](attachment/4528d3170ca396999412272f1d468015.png)
So both of them are not reusing the password.

![](attachment/7f124b72e1a41fdb4e5ceeef97aa5a87.png)
But there is also one more user in the home directory. Let's try him!!!

![](attachment/6b46e58522cc2d9a8756eed00412f6f1.png)
Permission denied!!!

![](attachment/2beb6ca5112e4e729f1053f62bafe1f9.png)
i can only read apaar's home directory.

![](attachment/1c5804efd21f485c4303a4d66728a6de.png)
Let's see how we can login as user "apaar".

![](attachment/214dd44fa56ac2b014b9a66aa48cc7b0.png)
images directory has two images, will be examining them because found no way as such for priv esc.

![](attachment/fb07884556395a86dd20135efdaa264a.png)
this is an image we downloaded, let's find for any hidden files.

![](attachment/25dae43d15b4b644643f486dfd2a26ee.png)
So randomly used steghide and didn't enter any password simply "entered" and got backup.zip file.

![](attachment/3a1084648ee0cd85a5db5a3222b5fdd0.png)
created a hash of the zip file, because while extraction it asks for a passphrase.

![](attachment/c1b05f12d194457ebfc8b4dd70343b4e.png)
"pass1word" is the passphrase.

![](attachment/ab1218b507f695e416ed8687f6d59eee.png)
unzipped and got a .php file.

![](attachment/0fb6f7d82c26827ece149bb72e739e2a.png)
found a password in the file.
![](attachment/a41089a13cbed9819caa81d44c5575d6.png)
So password was base64 and after decoding this is the real password. "!d0ntKn0wmYp@ssw0rd"

![](attachment/9b46b0e4187e86649a810481090f8909.png)
logged in as anurodh.

![](attachment/aff13e8c0f24004138ef5610ff0432c0.png)
it can run .helpline.sh as "apaar".

![](attachment/7ce58900adb4f312de00be4a4da42957.png)
same creds. used to login through ssh.

![](attachment/c1a336a6ad874390548d3f57d5ff0fdf.png)
logged in as apaar through script because the message that we will enter will be executed. I came to know that by seeing the src. code of the script and found that if i enter /bin/bash in message then it will give me a shell as user "apaar".

![](attachment/215faa3ead74fc30703da63096393903.png)
got user flag...

![](attachment/7b2dc2f17e600f40b082953ef69c58f0.png)
saw that user anurodh can run docker and an image existed so mounted the root directory in /mnt in the image and ran sh command in the container to get root shell.

![](attachment/817714e0c7a826c307b535baa5eba7e8.png)
got last flag....