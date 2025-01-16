**ip :- 192.168.122.68**

![](attachment/b17eba6501b95dc51075b7dab6a281f9.png)
machine on!!!

![](attachment/da7e2b82eaa932effac3f31b5508a5d2.png)
scanned the machine for some ports and saw that ldap is running. Now what the hell is it?

![](attachment/6979994b558d2040e5bc4430b56eb6a9.png)
so ldap is like an open directory service for accessing info about system, networks, services etc and makes administration much more easy and as well as vulnerable.

![](attachment/2a7240c249346016e3f049b8d85ddf11.png)
did some versioning and found nothing interesting as such.

![](attachment/72441b8a07bd76dc8ffe39dc1e575c12.png)
ran script name "vuln" which can find some vulnerabilities before hand and told only about a web page so went there to check.

![](attachment/16888d48ed32c409e1d6a9ff49439adc.png)
oops!!! got one!!!

![](attachment/f26f30d003655c9d419796035b46ddb4.png)
in directory fuzzing found some directories and static directory seems fishy!!!

![](attachment/fe3ad6042690ff7316a947e927bc0574.png)
in /static directory found these images and a file. Let's download them and see if we can find something or not.

Used exiftool and binwalk utilities to learn about the exifdata and if there are any hidden files or not respectively and found nothing!!!!

![](attachment/c326569697964f447ed3f28d69e7642d.png)
nikto told that RFI (Remote file inclusion) is possible.

![](attachment/beab7ff282465c51522c89d474edc6b9.png)
brute forcing and sql injection didn't work so did ldap injection to bypass login page because it is using ldap for authentication and not sql and using asterisk "*" can be helpful 

![](attachment/c3a5fe6c653648a818c60a18e00ace80.png)
in url it seems like a local file inclusion to me.

![](attachment/8233c83d01fc06f5f58f8e416818c304.png)
was able to view /etc/passwd file which confirms local file inclusion.

![](attachment/d56b7aa3f4ceb6acaf4d68c0a95813e1.png)
changed request in burp, /home.php?url=admin.php to see about admin and how authentication is going on and other stuff.

![](attachment/e80162676479b6520281d54d73df8a5c.png)
got something for our nmap ldap script.

![](attachment/b624ddb66af560c3366126ee974d4e3c.png)
by running a nmap script for ldap "ldap-search" in which we entered what we got from previous result and got username zeus and password.

![](attachment/86d2e6ecd17476037dce6ea3b0967ea1.png)
was able to login as zeus.

![](attachment/9b3b7369daff5183262136cfc1f23596.png)
can only run dpkg. Let's search on GTFObins for something.

![](attachment/bfc76e3920d66ecde395cd299e0cd6b4.png)
got root

![](attachment/fe9349f2f421063ba7a9dbc43f0e10ad.png)
used this exploit from GTFObins to escalate privileges.

![](attachment/1b15d3548ce394f496b844eb686751a9.png)
Got it...............................