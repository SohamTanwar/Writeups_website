**ip of the machine :- 10.129.114.185**

![](attachment/5596b12ccc9b405486f8d2266871b24d.png)
machine is on!!!

![](attachment/3d0c7f3ec2249ab2f4a41c6d9ffe1844.png)
only two ports are open!!!

![](attachment/962a791249498b106f73592b8e276f3e.png)
did aggressive scan and found versions of the services running on the ports...

![](attachment/a8da1d60c7e7ebf791d8086f5ced0285.png)
we have to add tickets.keeper.htb in our /etc/hosts file.

![](attachment/fcb9d2a9cad5fe68571b05cf01c0a473.png)
login page of request tracker is open!!!

![](attachment/edbd8d6757c567218987f69e3fdf6a95.png)
let's try these default creds.

![](attachment/69f8b532060718e34769738208ce6f20.png)
i am in!!!

![](attachment/0611535551f48636d5cdf9be823463ae.png)
in /admin/users found a possible username "lnorgaard"...

![](attachment/c3ae6e2ad6ad9b31834d64febdca0230.png)
Found a username and password let's try logging in using ssh with above username and password.

![](attachment/3af82ed883b082a1ba9dd12bfa002518.png)
logged in as user with ssh...

![](attachment/49f4bb8a52079dc1fff9b1c69aee45c5.png)
found 1st flag and a zip...

![](attachment/81a1627df60441089574a46db726184a.png)
after extracting the zip file found two files. Let's see what these files are...

![](attachment/6a1b2d7a33303ed5c43222125c62edec.png)
So .dmp is a memory dump file and that to a keepass dump file. Let's see if we can find a tool to parse .dmp file for master password for .kdbx file opening...

![](attachment/cca60fc7a6b1eb8ec7b54ef09fac6761.png)
came across this tool on github.com. Let's try this tool...

![](attachment/e558f7f72e401d082a682ff03edf7b55.png)
ran the tool and it gave some gibberish stuff, i don't know so searched it!!!

![](attachment/d03041700d3244d2546c1730cfea2bc9.png)
Let's try this as the password...

![](attachment/39d78083b57e88d43836e6e5830d59bb.png)
we need a password to open .kdbx file.

![](attachment/ec3973d18840cdf8162a481838dab9d7.png)
So added this as the password...

![](attachment/d95cab0f423cc3ff1f2c7f54b3213daf.png)
Wooh!!! got into the password database...

![](attachment/f41b1a97a493ae2323d9e524cf2dfc89.png)
in network section found "root".

![](attachment/7c92fd1584a1fb904a460f7d0cc5f65b.png)
Had a password and Putty private key for ssh.

![](attachment/519e98e405d904947f03547b3c873ef4.png)
Added this key in a file as password was not working, so will be using this to ssh into the server as root.

![](attachment/ebd27127b25c1abde0f8423867d9bbc2.png)
added private key in ssh authentication session in putty.

![](attachment/225fa6b1fddf8d82681ba68485289676.png)
add ip and then connect...

![](attachment/b4ae9967f697927fd5d59eb93ade3f2d.png)
logged in as root and got our last flag...