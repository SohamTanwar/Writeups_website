**ip of the machine :- 10.10.11.23**

![](attachment/df13e9017ba3516c4a6c8d83d8cfe802.png)
machine is on!!!

![](attachment/009a4bc2097ceb30f4e2db740f225297.png)
got two open ports.

![](attachment/c7b206de452968bafad39c135aab45b0.png)
did an aggressive scan and found nothing useful.

After entering the ip address on the browser, it is redirecting on permx.htb. So will add them in the /etc/hosts file.
![](attachment/ed191117af02d059075ddcd6e1fb402d.png)
After adding ip-domain combination, website will open.

![](attachment/7c3e9319e6338e641d240f9db7bf1ea1.png)
Did directory fuzzing using gobuster and found some.

![](attachment/8ea0c82f96a2c9019930315227950a32.png)
Did subdomain enumeration using gobuster. Redirected the output in a file because there are many sub domains giving 302 status codes.

![](attachment/71aec056bc198649a98004f30789ced2.png)
It had 5000 subdomains so grepped using source code 200 and found one.

![](attachment/89f5c73f3d20a2f3fa4495c72bdf6c4e.png)
found .css and .js files in all the directories, in /lib found them.

/css, /js and other directories gave some files of source code but not anything important so will be visiting the subdomain found using gobuster.
![](attachment/f11c3c436a25b7c3ee0e5922ebd6102a.png)
added lms.permx.htb in /etc/hosts file with the ip address of the machine and then we opened above web page.

![](attachment/1d5d81ab0adca0a57afb4b2b06f08f65.png)
in forgot password after entering admin as username, it prompted contact David Miller. So maybe David Miller is the admin.

So i didn't know about the creds so, tried to learn more about the this lms as we known that David Miller is the name of admin but it is not his username so we cannot do brute forcing, so tried to find some exploits related to chamilo lms and actually found one.
![](attachment/a5acf7d81812c546c663d7642b9ecea9.png)
So this CVE in chamilo LMS can help us to get a revshell without actually logging in so i followed the steps in repo to find what to do.

![](attachment/6476fff08644e9ff3787c05bcb7fad72.png)
first the repo said to do a scan to see whether the directory where we want to add our reverse shell can be accessed or not and it seems we can.

![](attachment/6ddbddb349a9078a12941b849e11a9a0.png)
in repo they have also given a path so let's go and see at this directory.

![](attachment/4a0b5150c087ae6dc4116b785358aced.png)
able to access it!!!

![](attachment/f61486e620c63eb35c5a0ef152a31711.png)
Now to get a reverse shell it was written to execute this command and listen at nc ofc!!

![](attachment/46b5f706d69136ef47e60b76b8c2e4e0.png)
after executing the command it will ask for ip and port and file names. Let file names to be default simply press enter, and added my ip and port on which to listen.

![](attachment/ebfeefbd94f8bf4216e739ffc15c366d.png)
Let's see our nc listner now.

![](attachment/85f0b3ae1d109f471b64636d632db094.png)
got the reverse shell!!!

![](attachment/f6477d982f2a4a6a34ad9aa6dc0b68e6.png)
in home directory found only one user.

![](attachment/eae74ae38d502aaf7041de44648b9263.png)
in /opt found a script.

![](attachment/bc80e220ae5143809d2de461d94fa81c.png)
saw the contents of the script and it seems that the script is used to assign permissions to the files and directories.

![](attachment/8db3093650d45fca6392b189d9f0edb6.png)
Didn't find anything unusual in cron jobs.

![](attachment/f203b708473b834b57ddd94c59397303.png)
found some SUID files. Didn't find anything to escalate privileges horizontally through SUID files.

![](attachment/1a1eb8a5138861ee30f144ed9ec2e31e.png)
/etc/passwd, users having bash as default shell.

![](attachment/76244070a538fad8340a0c22eb346b8b.png)
also ran pspy but didn't find anything useful.

So after manually searching for a while, in /var/www/camilo/app/config/ found a file named configuration.php which looked interesting and had literally information about the tables in database, there name, auth, cookies etc and that to in one big file. Seemed pretty sus!!! to me.

![](attachment/a10cb219b91453a548d8d1364ad88b9c.png)
And in the file configuration.php then found this interesting block of code.

![](attachment/75a4f3e78505290b8baedf3f11e16b2d.png)
in mysql server!!!! yay!!!

![](attachment/d1f43192e9277a0d46aa4e385221812f.png)
found two passwords in user table of chamilo database. Let's crack them!!!!

![](attachment/4f4893b2bb0ede2503f086bff26b4322.png)
Password cracking was taking time so used database password for the user mtz and was able to login.

![](attachment/da660753527c266a817205de40e83e6c.png)
user can run only one file as root which we discovered in /opt.

![](attachment/54892bbed5fe60cbee60e4374d7d544b.png)
created a symlink with /etc/passwd with pass in home directory of the user.

![](attachment/bf68322269345f2af98b5033bd50022c.png)
Then we can add a dummy username with root privileges in pass file and then we will get root shell and then further root flag...........