**ip of the machine :- 10.10.5.87**

![](attachment/df154cd4cc93574b78067c210a807af6.png)
machine is on!!!

![](attachment/d228c814a0ef8daa0ec59ae1849566dd.png)
Only one open port!!!

![](attachment/b8f7e90d0aa3b4014146e556c32542b6.png)
Now aggressive scan revealed the version of the server but is also indicating ubuntu's default page.

![](attachment/0e26350aa419565f093dcebc419bcc18.png)
Yup!!! Let's see if this version of apache has any exploitable vulnerability in order to get initial access or not.

Nah!!! Didn't find any.

![](attachment/de6c51b0a0a025cb88af40f765168de1.png)
Found some directories during directory fuzzing. "webdav" looks interesting.

![](attachment/f0625033520aa1309330d5991d5d6ac6.png)
Didn't know about 401 status code so searched and found something interesting.

![](attachment/94bee7d0389204126516c03160ca7e9d.png)
webdav directory asked for a username and password. Let's try some default ones like admin:admin, admin:password etc and nothing worked. Let's try to capture the request and brute force through hydra.

![](attachment/20006c5bb36eaac072431d41d897bacc.png)
So, after some searches, found out that webdav is a kind of service and found some default creds. to try on.

![](attachment/71e833b324dfc676f4cb421af164aaa8.png)
It worked and now we get a file.

![](attachment/c1e4f9d08d222514f08da8720838e251.png)
OK!!! So it's a hash. A password.

![](attachment/5d5584ce54204d1ab91c7deeaafb7494.png)
Unable to crack the hash. Let's try something else.

![](attachment/044ae43035bc289727e2d22c64e94398.png)
So, after searching about how to get rev shell to the server, i came along a blog on webdav on hacktricks. Let's follow this.

![](attachment/ac71acb830100d98c2140a973ac85e46.png)
Let's try uploading several files of different extensions using davtest.

![](attachment/c683efab9d6d88cb9034e73e8e294763.png)
Davtest is not available anywhere, so i have to clone the repo. manually and then test.

So, was unable to resolve dependencies after cloning the repo.![](attachment/281dbaf3c313136f412375d34f8a0ed2.png)
So, found it in arch strike repo. so will be downloading from here.

So, archstrike one also failed so tried from blackarch repo. and it worked.

![](attachment/41c78f5b6cae2fa5587b33d8a39fe824.png)
Let's try uploading pentestmonkey rev. shell payload.

![](attachment/c2c014f3d4669ecb4431b3ea4cd32c78.png)
So, ran davtest to see if we can upload any file with particular extension to any directory and that file then can be viewed from the browser.

![](attachment/ed578cc2bd0cdfc5a0708ac01d007035.png)
This means we can upload php reverse shell and get it.

![](attachment/ee0fe102ccdacf8967c507dbb7ab8a42.png)
So, davtest uploads some custom files in a directory to see and evaluate and we can see that webdav directory has the directory of davtest and also some test files in it.

![](attachment/69721e309cf9211f9c41d30a99dd6c85.png)
Then got to know about cadaver, which is a command line tool for webdav.

![](attachment/cee9f064235e36efcd574b0c6c71e025.png)
in webdav directory through command line.

![](attachment/ab6cdb21cdd39b3f9a4caa206aaee153.png)
Uploaded my php revshell.

![](attachment/aeffb933e02f75b683d199906745e137.png)
Let's initiate reverse shell.

![](attachment/a5b8b02247bd3ded095a1b5da12ce7e9.png)
Got it!!!

![](attachment/e50a295c24524581e301377e869ad08e.png)
Found two users in /home directory.

![](attachment/7e1eeafda499e0772c7ff55790f6196e.png)
So, found nothing in "wampp" user's home directory.

![](attachment/656a9b3a1f11ae433c7135cc9c7600b1.png)
Found user flag in other user's home directory.

![](attachment/a04e81f011a91e6505dd44772834e49a.png)
Did "sudo -l" and found that user we reverse shelld as can run "cat" command as sudo (with root privileges) so got the root flag directly.