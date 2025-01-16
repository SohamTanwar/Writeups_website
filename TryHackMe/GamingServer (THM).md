ip of the machine :- 10.10.167.136

![](attachment/ee8b5fc3072bce5b8edc2ce996042586.png)
machine is on!!!

![](attachment/41ac560fadf496b0211c994114cc05d9.png)
Only two ports are open!!!

![](attachment/4428e57eecff83e8b92292c08aed7580.png)
Did an aggressive scan for versioning...

![](attachment/3c8d8d985a1d6b01a14648b743d4e8df.png)
home page of the website, let's go through the src. code to see what we can find...

![](attachment/cdfda6a1b8e0fa22c19abaffda81e6ee.png)
Found a possible user "john".

Let's do directory fuzzing using ffuf.

![](attachment/c9207a39bec9b345d51e2c87f202aa71.png)
Found some directories to look at!!!

![](attachment/14e283afad5318ea13235beee09e51f8.png)
robots.txt hinting towards /uploads/.

![](attachment/3ca6dd0c6452f149bc185f69d2c4a1e4.png)
/secret contains a secret key.

![](attachment/20d6d7c42359929b2ed537aa964e5265.png)
it's a private key for ssh login.

![](attachment/f1adc1043ebda86236f4fe28938b41d7.png)
in /uploads/ found some files let's view at them first and then will try to login through ssh using the private key.

![](attachment/da963fb1d2fd889d04f82367204891f2.png)
dict.lst is a like a list of possible passwords.

![](attachment/858b08587178938475cac8f07bdd24af.png)
it is like a message for hackers by "the mentor".

![](attachment/749588ee134201357ad699def6e2b5d2.png)
Just an image.

![](attachment/a6e0f612d98ada2d54c16a6405f77bde.png)
using private key is asking for a passphrase..

![](attachment/353f0a6ad7dca7dd970c5290787f1526.png)
used ssh2john to create a hash and then further we got a dict.lst so used it for brute forcing and found the passphrase "letmein".

![](attachment/1f11fffc75d1448fd0287a6d81c77ed1.png)
logged in as user "john"...

![](attachment/0bf3053b749aa366b5da9745796f0535.png)
got our first flag.

![](attachment/b145188aeb67b86535a36a767c5ad3f5.png)
So we are into lxd container.

We are allowed to run lxd so will be following this below blog.
![](attachment/0ada42b898755a19b1b501c52b568dd5.png)

![](attachment/d327005611d2921948f651b87c906c92.png)
So will be using this to escalate our privileges.

![](attachment/4c43bd2ec2356e0c5b4487cee2f97278.png)
After following the above build steps, forward .tar.gz to the attacking machine.

![](attachment/3bbfa0892d8cc0ec9f14848006b02387.png)
importing image to lxc.

![](attachment/fb9e5e2d1392659bc4469e03214fa157.png)
we can see the list of images.

![](attachment/684b58055cbf6317098f64334607c5c5.png)
So first we are initializing the container and allowing it to run with elevated privileges basically privileges of root then we are mounting the resources from host machine to /mnt/root of the image and then starting the container. After this we are executing a command /bin/sh on it which will give a shell for the image. This image in container is running with elevated privileges so executing a shell means getting a root/pwned shell.

![](attachment/6520d3f007a055d9e70ab46305b987ec.png)
And became root.

![](attachment/d3edab67396deb0897ac6a7a249cb06f.png)
So, in /mnt/root, we have the root directory of the machine inside a mount point of the container.

![](attachment/ca27ef48a5aa453e2cf112a78e4ddff0.png)
So got root/last flag.....