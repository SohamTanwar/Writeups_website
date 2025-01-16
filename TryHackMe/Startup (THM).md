**ip of the machine :- 10.10.248.82**

![](attachment/97755572db8aa45c712be77cb86b066c.png)
machine is on!!!

![](attachment/e19dc89a01a86cbe53f349cd6de61005.png)
only three open ports found.

![](attachment/403ace13cfdcf91a72c9d0019a7a42ba.png)
Aggressive scan revealed some version info. and also revealed that we can login anonymously using ftp.

![](attachment/cf000aa36e17fd019193fa3f7017d76f.png)
found two files and a directory. Let's start downloading important attachments first.

![](attachment/478564c671efac7d31f20aa6b39acfb8.png)
in notice.txt found a possible username "Maya".

![](attachment/25227824f233b05267eaf87e0a56c17a.png)
"important.jpg" image's quality is pretty bad and is still around 256 bytes. But after looking at the hexdump of the image, i noticed that it has a file signature of .png image so have to change it.
![](attachment/1fc78f7662ed7f3b1ed9388aaff90a5c.png)
Let's change some bytes, according to .jpg. After somechanges file got corrupt and nothing found inside the file.

![](attachment/87114ec571de5b57b07bb73e236a6560.png)
Found nothing as such here.

![](attachment/70c0dcc48ee17933ac4e12bb34468cc9.png)
used ffuf for directory fuzzing and found some interesting directories.

![](attachment/60e11937dd6927e18944919b684a7f9e.png)
in /files directory got some files which we have already downloaded and analysed.

This means whatever is present in the ftp server can be accessed through web, it means that if we upload php rev. shell in ftp server we can actually invoke rev shell through web directory /files.

![](attachment/60fa5a1a9654e389bb023c1452457d1c.png)
successfully added revshell in ftp directory on the ftp server.

![](attachment/8cb8ed361f733669ef62e657f9476055.png)
So invoked the shell from web interface!!!

![](attachment/93f59c069f3d1fe33bac016db4cedc73.png)
got a rev shell.

![](attachment/56ad1b595e741f48473b9de01ee917a7.png)
found a possible user.

![](attachment/cef7d1444183b71d65dc3eb8b46755b3.png)
but in /home found another!!! and access denied to user's home directory.

![](attachment/464b0d11979ab285e6adf6da10f03e64.png)
found a file and what the hell is "love" maybe password of the user.

![](attachment/d1b01bc7407f725228a9c78c329ca593.png)
nah!!!

![](attachment/0849d603e4142664ee5ed45a5306c01f.png)
in incident folder found a pcapng file. Let's transfer it to our system and analyse it.

![](attachment/0a7cf7d644d9cb2081598504c8b5b9bc.png)
opened the file in wireshark. Let's analyse particular streams.

![](attachment/d31004af7931b4bd16687ac8f8d739e2.png)
in tcp stream 7 found a password.

![](attachment/edb9a911a3416c7bc95d0677f085005b.png)
was right logged in as lennie.

![](attachment/859434a379bdc7899218f9c9eab1ec7b.png)
got our first flag.

In lennie user's home directory found three text files, and now will view them step-by-step.
![](attachment/ae627bbce3b24d734d3473327bc2dbb2.png)
![](attachment/1911cca48cf85b78f873284e49fa9c30.png)
![](attachment/9c122493d31a7db1f28096d4c31380c9.png)

![](attachment/efce10b0ad49d084461bdee16a2ad444.png)
oops cannot run anything with root privileges.

![](attachment/f4177e93ca1d4f670d2533889e092449.png)
there was also a scripts directory in user's home directory and owner was root.

![](attachment/6a891eab4d4077c62ac9f6707d2fb5e8.png)
so viewed the script and found that whenever planner.sh script is ran, it will echo LIST variable values to the specified file and then call print.sh from /etc/directory. But as other we can only execute the script. Let's check /etc/print.sh.

![](attachment/de727b6a8ff84981d4b1c0c22a2d0c8b.png)
only user, we are logged in as can edit print.sh script.

![](attachment/193d48af094be3fe0eabd232493a43ef.png)
added a reverse shell in /etc/print.sh which will be called as root user and then we will get another reverse shell as root.

![](attachment/04b73a4445f2191b8482ccbaefb8ff35.png)
okkkkk!!!

![](attachment/06d15d00175fe016b73170afbc429e8a.png)
got root flag!!!