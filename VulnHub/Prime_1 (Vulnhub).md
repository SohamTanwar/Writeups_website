**ip address of the machine = 192.168.122.176**

![](attachment/c7656208bed0563c70c37de23b8e97c5.png)
First Pinged the machine to see whether machine is up or not.

![](attachment/9a6dd3039c345a2cd87275f9fded09de.png)
Did a service scan directly on all the ports of the machine.

![](attachment/d8643cdd42df831360642bccef3c4623.png)
Used gobuster for directory fuzzing and learned about some of the directories we can explore during manual web app enumeration.

![](attachment/732bd24bd235a91cbaa768cbee1dddb5.png)
Running nikto told about some more directories and also told that wordpress is being used here.

![](attachment/34abb6bee473309734bf66f81b4f6643.png)
In one file got a small message and any other directory and file is of no use right now.

![](attachment/a7cf82b08f2a6d30aee03e1b3b44fabd.png)
It told us to dig deep so we used dirb and -X to specify the extension of files which we want to find and we went for .txt only because to get any further hint and credentials .txt files are what we want to look for.

![](attachment/7971f3f529b76834c2acfa57079fbe06.png)
This file is hinting towards a github repo to find another file.

![](attachment/14304c73fb37394cbe19e2f7fe771da0.png)
Basically it is telling us about the tool which we can use for further fuzzing of directories. So basically trying all the options in it to find what we can get.

![](attachment/7604fa195844a7ba9627474960fc1501.png)
So in one of the options in wfuzz a query was done in index.php file for enumeration so did that by modifying the url of the webpage and hinted to use another parameter and that to on another php page. So now we have to another webpage so we have to do gobuster scans on each directory we found.

![](attachment/32fc57c0db0d5e3585a557c136007540.png)
So did another gobuster scan but this time of common php filenames and we know that we have to query on image.php web page now.

![](attachment/65d7dcabdc467090dca667a8d82e4dfe.png)
I tried to use a basic OS command and it told that we are using the right parameter.

![](attachment/1065f966a0a290a3c4d2f488672decd9.png)
When we opened the machine we got a possible username named "victor", so let's see if we can see passwd file.

![](attachment/d338a9f61164785c832aa5d5e5293454.png)
We can see in second last line there is a user named saket and saying to see password.txt file in his home directory.

![](attachment/404ed1d54d59a6e0a8a57fb560f2c8aa.png)
got a password "follow_the_ippsec"

![](attachment/78eb07f434476c71fab55ee9a540f381.png)
Now we have a login page at /wordpress/wp-login.php
Let's enter creds....  victor:follow_the_ippsec  to see if we can login or not.

![](attachment/57f688237de8d12bf16394890a9f3930.png)
Now let's see from where we can get reverse shell.

![](attachment/af260b92d5630a8a7286e8cd5f5388bf.png)
Ohh finally got a file where we add our reverse shell code to get a reverse shell.

![](attachment/19476983c43bf7233f6388ffc311b35c.png)
Added our ip and port for reverse shell using netcat.

![](attachment/c34614c7a12c4089942e61f83dea2318.png)
Now after saving the file navigate to /wordpress/wp-content/themes/twentynineteen/secret.php to invoke the shell.

![](attachment/aeb3efa4770e1320fcbe04f206069270.png)
Found out kernel version and OS so that can do priv esc using kernel exploitation.

![](attachment/19a753cd8b9728f5b65ffc111bd9a0d0.png)
Let's see what we can view.

![](attachment/c8a10d5472a90a01d8322abd59863238.png)
So we cannot access victor's home directory but viewed a file named user.txt in saket's homr directory and got a flag.

![](attachment/eaf076998d77feba514676d807e16350.png)
I used to searchsploit to see if we can get any available exploits to escalate privileges. Will be using 2nd one.

![](attachment/294c06ff7f10d3ca570ebb67c634eb7b.png)
Finally escalated privileges.

![](attachment/c44941126444ce192b8c61c8afa07a84.png)
Finally got the root flag...................