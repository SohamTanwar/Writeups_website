**ip of the machine :- 10.129.231.161**

![](attachment/1e156b1c4c30f8f90ec2349a598d4e2d.png)
machine is on!!!

![](attachment/0235e59fc3095f5f2b71d9a832c8dcf7.png)
got some open ports!!! Let's do an aggressive scan to find out the version of the services running on the respective open ports.

![](attachment/4e39f9efd55dcb73b24ff3984f8d2093.png)
Got the version of the services running on the ports...

![](attachment/f38d79169a9b1b5e149090750ae66c05.png)
Let's ip and domain in /etc/hosts file.

![](attachment/a98774f9233e3104eaf65f070177cecc.png)
Now let's open the website again...

![](attachment/728761962730ce019603bc40b0068eff.png)
http and https both are running this same website and found nothing worthwhile on this website, so let's do directory fuzzing using ffuf.

![](attachment/f104da25293c8178c6b2092ee4745cd4.png)
It literally showed that all directories are present that are in the wordlist which is not possible so maybe there aren't any web directories. Let's try subdomain enumeration using gobuster.

![](attachment/443956789d0f357a0538b21688eba1a0.png)
No subdomains as well, now that's strange...

![](attachment/53a004b627b9d8846dd265f546839cc1.png)
So when both of the fuzzing scans didn't work, i searched for common .php file names and found all the files as redirected to somewhere which means they do not exist and didn't find any...

![](attachment/e0be83cb9aa7f646cff19a64356756d1.png)
As no scans for subdomain and directory fuzzing were actually working and there is no anchor tag in the website to capture any kind of request to analyse it, went to storage tab and found JSESSIONID and the value has .jvm1 as the extensions which seems good enough to move forward to the next step.

![](attachment/ab0b19d527d5ac84d281787f5de81492.png)
So, when searched on google, one of the results was saying that it can be apache OFBiz...

![](attachment/948cc412ea3816e4082dfc6fd630e497.png)
Then in footer section of the website it said Apache OFBiz thus conforming that web application is running Apache OFBiz.

![](attachment/1da277b9b75556dea83bb289e3a16841.png)
So, did a directory fuzzing again but the wordlist was "apache.txt" this time and the results were limited. But again every directory and web page was pointing to the default web page.

![](attachment/aef928164d8f0ac36077eab45f79faa5.png)
So found this repo on github with a scanner like tool for rce. Let's try it!!!

![](attachment/f26faba42221362166b880ae0dab8169.png)
Tried to see /etc/passwd and it worked... Now let's try to establish a reverse shell connection now.....

![](attachment/5b0aa1e926bace3c835d5350fb1e7e57.png)
Didn't use any reverse shell payload, simply used netcat in order to execute a bash shell command and get response on my machine...

![](attachment/d5b51580713784d9b79e65a8ea2e4e58.png)
got it!!!

![](attachment/cec208522745b82e0d91adef813f2427.png)
In user's home directory, got user flag...

![](attachment/8e6fb5ea91abd42ffd209e674a5d4aa2.png)
There are a lot of files and directories in the directory we reverse shelld....

![](attachment/530de2b53f89d233f8f9abcc844c196e.png)
In framework/security found a file revealing certain properties related security like password is encrypted using SHA, min. password length etc.

![](attachment/57335a0d5b62748123e6539ec7672d86.png)
So came across repo. of apache OFBiz and saw that derby is an embedded database based on java and is stored in runtime directory...

![](attachment/200f92d4e63ddcf574369b5a6e28de3e.png)
So to connect to this database we need valid url, appropriate drivers and a command named "ij".

![](attachment/14b42c59c88086accd5afbc10503a056.png)
Made a tar file of the derby directory in ofbiz and got it in my system.

Oh man!!! It's not easy to connect to the database straight simply for a file or folder like sqlite3.

![](attachment/b0d2ca8c839fd0d458aaf79517d164ca.png)
I was fed up troubleshooting, but then i noticed while creating a tar, it archived lots of .dat files, let's see if they can give something interesting...

![](attachment/b600bb1d0a423494de2b856f0f3158f7.png)
Hmm, this means we can find something interesting in these files...

![](attachment/a10da724c42f74dc522ec888af67917b.png)
So used grep command to reveal the password... Here, -arin flag means binary text, recursively, ignore case and printing line number and -E for extended regex.

![](attachment/cb5d38b5bbb8d63b8191263ba3c77770.png)
got this password hash and seems like a custom hash and not sha...

![](attachment/e5801a6a78739f6f9dd9d9dfc28cd4e5.png)
Found a lot of directories in crypto directory in framework/base and much more deep in that...

![](attachment/007ccbbad8173e88bb711de7e2dca6b2.png)
Looking at the src. code of HashCrypt.java and looking at the compare password class. It looks like it is calling doComparePosix class.

![](attachment/4306dde81f7ab94ec87ed2540f4d49a1.png)
So, here now hash type, salt and something something is getting seperated and then another class is getting called getCrypteBytes.

![](attachment/afd5e3243ab1b83c29989493b0ff514e.png)
So, it is encoded into base64 while replacing + with "." and getting the hash type which "sha" to further encode it.

![](attachment/84b7aaeba26b98f434f313b2480c2122.png)
So there was a custom encryption and at last got a hash that is crackable...

![](attachment/69ea11081a5940e0002209721389c72f.png)
Got a hash and also added the salt.

![](attachment/d5ce07bb541e5120ac960a4006fa2d2d.png)
Cracked the password as "monkeybizness".

![](attachment/eac1b8bf69ca33e146ad48ede16e9c82.png)
logged in as root with the password...

![](attachment/ef540eccea322a91321cdea4ab4437be.png)
Got root flag...