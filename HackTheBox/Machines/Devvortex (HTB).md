**ip of the machine :- 10.129.229.146**

![](attachment/a53129460cd0675af5584c9fb4318907.png)
machine is on!!!

![](attachment/0bbf544b8a9d41a4f15fb2995e924df0.png)
As usual two ports...

![](attachment/1715838edd8f25207ebf9aa29305a3c9.png)
added ip with domain in /etc/hosts file and started exploring the website manually and didn't find anything on manual enumeration.

![](attachment/3c3496ae9daa7406f7545aa0f1e3ac5d.png)
Just the usual directories....

Let's do subdomain enumeration...
![](attachment/85ba9290ae13ea4d5b7ae094c7d575fb.png)
Used gobuster and found one subdomain. Let's visit it!!!

![](attachment/1ab284b42dfbdcf0d5bcbb7f98542d8d.png)
So it opened another website and again manual enumeration was useless over here and let's do directory fuzzing then.

![](attachment/c695a60e129b79f94345bc1b7adc0b62.png)
got a lot of listings.....

![](attachment/8e5397fdfb5725539ea1bb95a258b10f.png)
Found joomla running in /administrator.... let's try finding default creds...

![](attachment/ad1e3fb5ca4fa71e0ef35afad74fac57.png)
Default creds. didn't work but found this vulnerability, let's test the system for it...

![](attachment/48748724ee1f64d9416a91e17612e392.png)
Used curl and got a lot of text in bottom...

![](attachment/0a1f3f3d4a54484983c5b064e2debe48.png)
So, here got a possible username "lewis" and email of lewis.

![](attachment/a894a02f6fd6ed2a42f1e53937c9cbdf.png)
so used above curl command and then found "lewis" password.

![](attachment/862cb1f128e4983a251a0e0948f10a98.png)
Found the password....

![](attachment/3cd9b19e5e7d8a375e295b47833c9034.png)
Logged in as user "lewis"....

![](attachment/6abf801513c8b9485c914c7555578f25.png)
So in system > site templates found some configuration files, and we can edit them and also found a possible user "logan", so will be changing error.php.

![](attachment/9af32851795692be316b650a0f984fb9.png)
So in error.php added pentest monkey reverse shell..

![](attachment/43ba6f13ac431583b3236d5c59627be1.png)
after saving do this to initiate reverse shell through error.php file.

![](attachment/8f0cf0f3b5ea6004e3152cf05cab83f6.png)
Got rev. shell..

![](attachment/dcc151ab57461cf826675a67d597cca8.png)
so in /var/www/dev.devvortex.htb found database creds and database where other user creds. can be found. Let's try mysql now....

![](attachment/1d7c253c1903606ab5de7ad9bd860c8e.png)
it worked....

![](attachment/90ba21e71b115cb52b74f132f9f1ffa2.png)
In joomla database found some tables with name "user" in it...

![](attachment/f52a9aff6d186994c1bc3cf0e775c1f3.png)
found "logan" users creds.... Let's crack it!!!

![](attachment/fbb5965cb9565fdf14b1b95c9d2b8ebe.png)
So will be using hashcat to crack the password.....

![](attachment/e527710c04588481f4803dd41ed9b4e2.png)
Cracked!!! got it!!!

![](attachment/b9516b2ccf70f14db2292f36f5d15396.png)
Logged in as user "logan".

![](attachment/af09a89e1ab94e42b9e25f20f3af8414.png)
Got our first flag in home directory of the user.

![](attachment/44304496dbeb45f39e20dab046728010.png)
So user "logan" can only run one command with root privileges..... and it is "apport-cli". Let's search how to escalate privileges using this command.

![](attachment/f7f3578c31aeb223982e773824bc4acc.png)
So came across this blog on medium and will be following it!!!

![](attachment/40c1881e3da1fc200b0a736a8f53a1b3.png)
First click "1"

![](attachment/d0ef4e20ea274f3f7d5614e2432468fa.png)
then "2" and wait...

![](attachment/7c37528837bac7a3cc87c9ed4de62eb7.png)
then "V" and when colon ":" comes type "!/bin/bash" to successfully escalate privileges...

![](attachment/f8ba42ff67e367c7065bcfbb72d73e32.png)
Got last flag in /root directory.....