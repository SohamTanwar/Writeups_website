https://app.hackthebox.com/machines/Lame
![](attachment/8ee662e72ddb7c0acf00e45de4569ad3.png)
**ip address :- 10.10.10.3**
![](attachment/ba1542b2c96648aec7cbf5bdf1f08c3a.png)
First we did a ping scan also known as "ping sweep" to see whether the host is up or not.
![](attachment/03a1c52b66649fdbcb412d5669901884.png)
Now we did an all scan (-A) to get the os information, version info and traceroute information. "-Pn" was used because we know host is up so there is no need of pinging the host and directly start scanning, and '-T5' for speed and min rate to send 10000 packets minimum to speed up the scanning process.
![](attachment/5f7ab9e5552eaead961b380872a1b200.png)
So, we can see Samba is running of Port 139 and 445 and FTP running on port 21 with version vsftpd 2.3.4. The scope of exploitation in this case is in FTP port and Samba ports.

So, first will start by exploiting FTP.
![](attachment/d67f9f3880ea591323e34d392f8585df.png)
I searched for vsftpd 2.3.4 which is a backdoor command execution exploit on msf. 
![](attachment/5ba59848b9c17523551c72a24b4284a9.png)
Also tried to use it but failed because we don't have a password to create a backdoor session.

So now we only have one option. We have to start exploiting SMB on port 139. 
We need user and root flag which means we need a shell to get those flags.
So, Let's explore what possible vulnerabilities this version of SMB has and what possible exploits we can find to get a shell to execute OS commands.
![](attachment/f5fdbc7f2c3ff73c769c66d376f7d330.png)
So searching CVEs on cve.mitre.org and found this vulnerability which allows remote execution in server. 
Let's see if metasploit has any module to execute the task.
![](attachment/b44df63cdd94d42f305133b9c8f8535a.png)
So after a lot of searches i was able to find the exploit because you cannot get it directly by typing "samba" or "smb" in search and not even "samba remote", we have to be a bit specific.
![](attachment/4500465584f6e974fa324f7bd41ddcc4.png)
After setting all the options click exploit.
![](attachment/0da0ac92c3846c292eb092c9c16d7c33.png)
We got reverse shell prompt.......
![](attachment/90bc476d83ac8850bd19fdb037503a4f.png)
We used this python one liner to get an interactive prompt and we can see we are already logged in as root.
![](attachment/7a82a0033137f9e8cdf0aac4686eba34.png)
so here we got one flag of the user.
![](attachment/de5ba7233a8e48f520fd2a18f0552e36.png)
here is the root flag.