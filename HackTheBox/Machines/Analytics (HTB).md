**ip of the machine :- 10.129.4.229**

![](attachment/90c90e5c17be6ad26b8cd0cd7b2f6046.png)
machine is on!!!

![](attachment/0597b70d58430f0a960adf52c15c990e.png)
Got two open ports!!!

![](attachment/0426406670b6e9b18fe4b778d499d607.png)
got versions of http and ssh using aggressive scan of nmap.

![](attachment/064c43eb9ccdd1a701e81c8d91405f72.png)
add ip with domain name in /etc/hosts file and let's do manual enumeration......

![](attachment/38b895bc42fdd6409d4a253f65e5c501.png)
Found these menus in the side bar.....

![](attachment/d6336d60cb2562240f6cdd13f1c1a2e8.png)
So after clicking on "login", found this login page...

![](attachment/9cf7309f38add8c95a5182bac3618884.png)
So didn't find any default creds. to the metabase login page and searched for any possible exploits and found this, we don't know the version so let's to hit and trial and use this as it came first and is one the most recent one of metabase.

![](attachment/252dc17d322149ee93acdeccdfeff7bc.png)
So in the exploit enter url, setup-token (can be found at /api/session/properties) and command which in this case added reverse shell payload.

![](attachment/e8c8c44b0db51b57f87ec79366de2211.png)
Got reverse shell.

![](attachment/f3e681f57989086c062063b585e313f9.png)
Got a user but no user.txt in the home directory of the user.

![](attachment/e014b36943997e4c2aa9d0e48e96ce20.png)
Was unable to find anythin even after using "find" command with user.txt as the parameter and then checked environment variables and found this user and pass. Let's try to login as this user with id and pass.

![](attachment/d37a9644e84e854d3170faf7b3e85316.png)got it!!!

![](attachment/b1be29f41bff554154359bbf71d68b9a.png)
got our first flag...

![](attachment/3872583241be49a6281b19c9849ebb7d.png)
Didn't find anything worthwhile in user's home directory and as well as user metalytics cannot run anything as root user and as well as no other user...

![](attachment/1b11fb7eb601230adc230f7aae7a5870.png)
No unusual cron jobs are running.

![](attachment/e8d4bea0b9d741df043ba99e552b2abc.png)
No other user confirmed.

![](attachment/3cfb9269210545ecee335c799010bf13.png)
No SUID and GUID files present that can help in privilege escalation...

![](attachment/c1dccd4577d28a708a390dc7544edf99.png)
Kernel exploit can work but will look at it afterwards...

![](attachment/17c9e8bbc4043ac37f6f48472ad2718a.png)
in /opt found a directory which cannot be accessed...

![](attachment/de6577b8b5bb1b197394312db4e340f8.png)
So after searching a lot and not finding anything found a way for local privilege escalation using kernel exploit.

![](attachment/c50166fbf089ca8b9d86ea32f4bb28d9.png)
So got the exploit in compromised machine and ran it and thus escalated privileges vertically.

![](attachment/0b0f1d915331692e7f38d19bdcb1e531.png)
Got last/root flag...