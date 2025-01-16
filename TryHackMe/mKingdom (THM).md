**ip of the machine :- 10.10.109.191**

![](attachment/e9b601e588ff7d5e19ec6652b0e3becf.png)
machine on!!!

![](attachment/f3f55f73d57386d1f6a1cc079260244d.png)
only port is open but what is it??

![](attachment/c492fda5e1639c33998992ada04004b6.png)
an http server is running at port 85.

![](attachment/35c77cbe6b0dd982740d1703255ea4e5.png)
found nothing on inspecting/viewing the source code.

![](attachment/2f5ff7e064599d8f9f093ac52ff78acf.png)
on directory fuzzing found these results.

![](attachment/a83311780408b6cdb0e3226b45edc82c.png)
after going to app directory found this web page.

**changed ip :- 10.10.84.11**

![](attachment/5aa9f0a4c650175fc5d9c84ffd4af4a5.png)
saw a blog and /index.php/ in url. Then tried to inspect the source code.

![](attachment/551b3b602a57c3c186c0f3f54d4bfbb7.png)
found this in src code which depicts the directory of the image.

![](attachment/044c8763a640bce9f1f620f0d94cf129.png)
also found this which told about the file extensions allowed.

![](attachment/f8e372d99b6cf6f4a2ca420341bd80d0.png)
in footer section of the src code found a login page link.

![](attachment/6eead8cdfac1db041c20d06371805f6b.png)
found a login page.

![](attachment/92ce098724e8f290c1b04e7c4ab36af3.png)
oops!!! logged in with admin:password creds. didn't brute force using hydra.

![](attachment/14ee730b916b24846a3f5ae2ed8f0027.png)
huh!!! what is concrete5??

![](attachment/13fcecd7e772ce3f8c63540447a83c9d.png)
it is a cms system like other vulnerable php ones. Then, let's search for any possible exploits.

![](attachment/54a39f70bf82b4b713bd2610e3737ace.png)
found first website to be helpful to get a reverse shell.

![](attachment/3c63fa0c588127b7ad1f0221fad10250.png)
go to allowed file types and add .php extension and save it so that we can add a reverse shell script.

![](attachment/c3c75db2d54d8667e57af7eba353017d.png)
now generated a reverse shell using msfvenom.

![](attachment/7153930e3e2543c53acf276ec14ece8f.png)
go to file manager and click on upload files and upload the reverse shell.

![](attachment/2d5240aae1633f02b8552f140caba473.png)
uploaded the rev. shell

![](attachment/5a182075e3a37d7b652d5998e176dae8.png)
clicked on the file and got a reverse shell.

![](attachment/dd60437227507c801f2a9824228ed9e6.png)
able to access mysql database with no pass.

![](attachment/8a3cce3e817e503ce7d8a26b1664b8b2.png)
found some possible pass and a username "toad"

![](attachment/cd4f268cc7aa0dcd2a3c8db6680aba01.png)
got another possible username "mario" as well.

![](attachment/9fa0bb5cb8233e6d5f18fa510517cb0f.png)
got password for the user toad.

![](attachment/00f48d61588684905a338883bcf97fe2.png)
was able to login as toad.

![](attachment/2b4d7af08fd53a4c586dcb683fbac558.png)
only found a file with this and nothing much interesting. Let's try to login as another user "mario"

![](attachment/d4f4ef9e698978c28829a6b4e069c3e9.png)
Well!! we have to login as mario. Toad is useless for us.

![](attachment/2974cdd82b352d11b0bc425eacf46165.png)
in env. variables found a strange base64.

![](attachment/893645b0cd158b3d6165becfc974b14e.png)
![](attachment/5d0d2dc1765c8a8257156abe547aafb5.png)
logged in as mario user and mario can run only one command which is id.

![](attachment/9c5813433ab61cb568e0007278b80d2b.png)
ran pspy script to see all the bg process and found these running after some intervals.

So it is downloading a script known as counter.sh from a link and executing it.
![](attachment/3d6cd799b6e5506c83037e84f9baeb59.png)
/etc/hosts file was writeable so added my ip and started a web server on the machine at port 85 so that it can fetch a script with same name and execute it.

![](attachment/4e9042d0e8c4c6ba186b8d26b71efcb6.png)
added shell in the file with suid permissions and after the file is fetched and executed /bin/bash will get SUID permissions and that to of root user.

![](attachment/88bde9f1d141f8244ef3b05abe73dbaf.png)
bash shell got SUID permissions, so executed the shell with enforced permissions and got a root shell and then root flag......