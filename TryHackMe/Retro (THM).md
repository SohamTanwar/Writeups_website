**ip :- 10.10.103.253**

machine is on and it is written it won't respond to the ping so will start with nmap scan directly.

![](attachment/dac41c52178fc2a39e8374ad0129b767.png)
Found two open ports.

![](attachment/6a0db277921a67c20fbfda4ec1d54e2c.png)
did aggressive scan on the ports and also searched that RDP (Remote desktop protocol) is running at 3389. Let's do some directory fuzzing now.

![](attachment/dc436a4f9241f6c48d23305757488621.png)
oops!!! didn't find any directories using gobuster. Let's try wfuzz or ffuf.

![](attachment/ad0472f68bfd6b4a03efc72c916a05c4.png)
using wfuzz found one named "retro". Let's go and visit it.

![](attachment/50e36a2bac50806873ad6f335f14f55a.png)
Hooray!!! found something.

![](attachment/0513772b8efa9582d0a5ebe0a2507982.png)
with this block of code in src code, i am hinting that wordpress in some way and we should do directory fuzzing in /retro directory.

![](attachment/96264523c5f5865bac60180d9bf90495.png)
wpscan gave some positive responses thus confirming that wordpress is running. Wordpress version 5.2.1 is running which is vulnerable.

![](attachment/edf363f81d9e0d57d33efd6518c31463.png)
Tried to go to the default login page of the wordpress which is wp-login.php and it exists.

in /retro found that all the blogs are written by a user named "wade". Let's try it on login page.
![](attachment/6291350f3620f953aff55f7dfabd2e7a.png)
password was wrong but atleast username is confirmed.

So will brute force it using hydra, either will go for rockyou or will create a custom wordlist using cewl. By both methods failed terribly. So had to study blogs uploaded by the user "wade" and have to do a lot of hit and trial.

![](attachment/e6aa20a91a566e195ff696a30dbaa50a.png)
in one of the blogs it was written ready player one so searched if user wade has any relation with ready player one, and found this. Wade is the protagonist of movie ready player one.

![](attachment/5b399b467e9fc7f28bcca42dfcabe5cc.png)
The user said in this post that he constantly mistypes the name of avatar of wade in the movie, I have watched the movie and the avatar of wade in the movie was "parzival". Let's try this as password.

![](attachment/79e9b2538fc5a1fcb0f475e182493cc7.png)
hooray!!! loggin as wade.

![](attachment/73aa4a03c32591e9e7096f67be0218cc.png)
was able to login using rdp with wade:parzival and got user.txt flag.

![](attachment/01dcddb7beb3316f4537da15c293292f.png)
used whoami /priv to see privileges and saw that "SeChangeNotifyPrivilege" is enabled. Let's see if any exploit is available for it. Didn't find anything useful.

![](attachment/a5bc3a1848f1af2a4b786eda31795eef.png)
added reverse shell in one of the configuration (.php) file for reverse shell.

![](attachment/6860e649f42daa315d06def4b3e7c917.png)
got it!!!

![](attachment/bcf0fce7306c37b53d2acf3cdf20046e.png)
after getting got some info. about the privileges, as "SeChangeNotifyPrivilege" didn't had any exploit for priv esc. So will be checking other two.

![](attachment/85eabae9956b7cc6cd0963744c02ad6b.png)
found an exploit for "SeImpersonatePrivilege" 

![](attachment/596b4ca01b1534e9c7b2528aef3bb6e8.png)
printspoofer.exe didn't work.

![](attachment/a32faa4170c3743f65516f3660bb77d0.png)
So now will be using this blog by hacktricks for priv esc using juicypotato.

![](attachment/e4f48940c12c1b89a5474bd212db6cf0.png)
got some systeminfo first.

juicypotato didn't work for me.

![](attachment/148702e110f7360abdc6d258bcf5ba64.png)
then went to google of the rdp desktop env and found a cve in search.

![](attachment/e0cc8c421b2dc54cf4bec3eabbb5b3b8.png)
also saw that the recycle bin is not empty and found a software.

![](attachment/a0e62f1e7f5c4083e865de5daa4c5d6e.png)
and this is about the cve and how to exploit it.

![](attachment/7980876561b9004bb094e9130329faff.png)
it triggered the UAC prompt screen after restoring and clicking on it.

![](attachment/48d04af339ae084893752ab64629cc3a.png)
Then followed the second step and clicked on the "show more details" and now we can see publisher's certificate.

![](attachment/f3a5a86282e7b542f3afd61fd401df61.png)
we can see "issued by".

![](attachment/c52e960a85ad876ede5426ded96d8cc1.png)
now we can see "how we want to open the url" pop up and this also didn't work.

So i failed to exploit manually so now will be using metasploit for priv esc.
![](attachment/583aa81eb7b75bbf2030e99ebc89eb3a.png)
so after some research about the vulnerabilities, will be using this. It is basically juicypotato only but have to add options of juicypotato to achieve priv esc and again it didn't work.

![](attachment/60ebd946eff06d03b0692e523e466d2a.png)
Got root so after searching again came across a kernel exploit with an associated CVE and used it and got root shell.

![](attachment/baafb6a16c8eb47738f8f98475dbd8d7.png)
this was the CVE associated with this exploit.

![](attachment/384f09b92c1d130ba73e5c236eaaba00.png)
got the root flag.