**ip for the machine :- 192.168.122.42**

![](attachment/3eb79618cfd9e69bca289255d79519fc.png)
Machine is up.

![](attachment/3a2f12770fa842085b64861f7273327c.png)
got some open ports let's do versioning scan.

![](attachment/2e2e325398c5c0441217a27f4ad96476.png)
Did some versioning. Will run gobuster now.

![](attachment/e7b06fec43c81c9e024bcbf329f5753d.png)
gobuster scan results show some files and directories.

![](attachment/12aa33f7fb46421b2c23a2b304a85a17.png)
Nikto scan results. Now let's start viewing these files and directories manually.

![](attachment/f604dd0568c1e65032f9cb41a8564335.png)
robots.txt pointed towards a specific directory.

Nothing found in the /secret directory.

![](attachment/7a5b5023ea106f0bec331eec46f0f9ad.png)
was able to connect directly to the ftp server and got a .pcap file. Let's open it in wireshark.

![](attachment/08228a5a2057bdbcab2b71b68e632572.png)
Followed TCP stream and got something interesting and possible creds and also a file name so we can export object or simply the file.

![](attachment/be8830369223cffc15cc2804c9ddde24.png)
got it.

![](attachment/b8059186d0f8d282ed1d6ff4f20acfcc.png)
Got some info, possibly creds. but of where......?
These creds. not working while trying to do ssh. So after some manual stuff found that it is a directory.

![](attachment/32f652fb1e3774d2c98bdc74831e25c1.png)
got another file.

![](attachment/da5d84cfb7c0e9e0bd2e9d6ab347e1ff.png)
the file was an executable so executed it and got another directory.

![](attachment/ef683ff318967eac06153440891ef176.png)
Got some other directories in one found one.

![](attachment/0ea99702ac4377025ac4cba6ce738fff.png)
Got possible usernames file.

![](attachment/db91bc4866bcb3c173c7f778b7a575b0.png)
Got this in possible passwords file.

![](attachment/ba7735c6cc02c72be18f901763a534d4.png)
Did a lot manually as hydra was showing problems.
and found possible creds.
overflow:Pass.txt

First saw SUID, GUID and World-writable files.
![](attachment/cab96f673dec6a5bc8a26cce36dc0252.png)
found a file cleaner.py to which we can write.

Now added a shell in it with SUID.
![](attachment/4c7608f81b0c9052eacdab049d335b48.png)

![](attachment/873f8cef514bd74df3908432d3bf2673.png)
now ran the shell and got flag.........................