**ip of the machine :- 10.129.232.66**

![](attachment/72aa44e5a6a2c99d27ef04e56544af15.png)
machine is on!!!

![](attachment/c12fcf47aced1f3404c496fc6025d59b.png)
Got only one open port and that is also running a web server.

![](attachment/fd2c163b0a630937b1ea8b1bdd633828.png)
Did an aggressive scan on the port and found out to be a python server.

![](attachment/9e8310defe6a64b4353c989c9d5e5b16.png)
So, it's like a gaming website with domain mentioned in the footer of the web page. So, let's add domain with ip in /etc/hosts file.

![](attachment/e8f211aea1380f5d29979ad408ad0033.png)
Tried to do web directory fuzzing but failed as it said all the directories in the word list exists which is not possible.

![](attachment/31d08631f9b1ffbc291fc3e5486956dd.png)
Subdomain enumeration also failed, there are no subdomains as such...

![](attachment/230bea275544a13dd92ae5df7188aa49.png)
Found a sign in page.....

![](attachment/d6a88d67255d57a4760d184ab97c227e.png)
Just added some dummy creds. "admin@gmail.com:admin" and will capture the request using burp.

![](attachment/c5f4ebfd5f03fee0447da1f0cdc335c7.png)
Got the request in the repeater. So i know that if any login, signup or forgot password page is present, try for SQL injection as it will communicate directly to the database in that case. So, will be trying for SQL injection.

![](attachment/bf1be7f7580f026e32bd3b504ccbb6e5.png)
So normal payload didn't work, so went for boolean based SQL Injection and added a basic payload to make the query "TRUE".

![](attachment/7294fc82b3a604c3bd86ddf7b36d0fe9.png)
Response showed login success. So, now will be saving request in a file with .req extension and will be using sqlmap in order to get credentials from the database.

![](attachment/22e7187e96b84668ea057508f9277f93.png)
Removed the payload and got the request.

![](attachment/74437ccb84fc0ede0741767d36d04da5.png)
Now sqlmap will try all possible payloads.

![](attachment/e13ffbacc24f35d6dfdf1dd466da21d3.png)
time-based blind payload for sql injection!!!

![](attachment/ba572afa0042dc81428a08cd017c9283.png)
Let's check for all the databases present on the server.

![](attachment/eb5cd2956aa5c80bc3c403f519d81e97.png)
Got two databases. information_schema is obvious, it would be there. So, will be going for database named "main".

![](attachment/99680d5dcf6771249f49accb75f25a8a.png)
So now will be dumping all the tables and their entries in main database.

![](attachment/6ddaeb42aecab6d5ead8099845b8f9fd.png)
Ended the sqlmap scan as we got the table names blog, blog_comments and user. SQLMap takes a lot of time and it was printing blog table so ended it and will be viewing the contents of "user" table only.

![](attachment/7d3565badc80cb5a994a64eb1c72a4b1.png)
Fetching columns and entries for database "main" and table "user".

![](attachment/8b622438fb60b2f7bca9c115c5e081fc.png)
Got admin email id and password hash.

![](attachment/dbb9204a7c7c0ffb5651a242895b03ae.png)
got the password, let's login as administrator now.

![](attachment/c3b51fdb57b876418b06f72b2a0ed2b8.png)logged in as admin now.

![](attachment/d66cb3c306b3f34eaf7d04b6cabd35dd.png)
After clicking on the settings page it tries to redirect to another subdomain, let's add this sub domain to /etc/hosts as well.

![](attachment/10130cf040537c5d427d2e6ad04419f9.png)
Trying creds. of admin with same pass.

![](attachment/4c4cead580bcc144327ed667816f2ee3.png)
Logged in!!!

Let's search for any possible vulnerabilities in Flask Volt dashboard.

![](attachment/4276ae1913f3a8292f762289bbba1f72.png)
In search result i saw something called SSTI.

![](attachment/88d5efbaa645f4c74e0835201f847f70.png)
Server side template injection. It is basically injecting malicious payload in the template which rendered at server side by the application and is common in python web framework flask which is running. Let's try for SSTI then.

![](attachment/c07e2983c1cacc41ae04d79793374e6c.png)
SSTI is usually different for different languages running on the back end, so when i typed SSTI flask it was prompting Jinja2 on hacktricks, so search "jinja2 flask" to see there relation and found out that flask uses jinja2 as the web template engine.

![](attachment/6261d2685853737428a07d3f5480e154.png)
Got the blog at hacktricks, so will be trying the tricks in this.

![](attachment/831195034222312a8f65e80599d39d6a.png)
So got some ways to detect SSTI, so we can try adding  the payload {{<any_expression>}} to see if it evaluates the arithmetic expression or not.

![](attachment/d492eaa0e3c0327a4fbf46798e6dafd3.png)
So in settings tab, found that we can enter our full name, while birthday we have to choose and it checks for phone number, so we can only inject payload to full name only.

![](attachment/175ac8a72d0b1f96c912ec5b182eff8d.png)
So added the payload and after clicking "save all", it evaluated the expression thus, confirming SSTI.

![](attachment/696e1c99a60c5b238cfa7e0beb30bd11.png)
So, search for "SSTI to RCE" and found a blog on medium which gave a payload that we can add.

![](attachment/0961a7dec946d8a9c6e68bbfa2d7d54f.png)
So added the payload to see the directory listing of the root directory and got it.

![](attachment/1bdda98757ff33dee0fcfeb35b6ba60a.png)
So added this payload and it didn't work for the reverse shell...

![](attachment/fbe59ce52ea3c2584bf73a68df4f4733.png)
So added this payload and got rev shell. So i base64'd rev. shell payload and then decoding it and piping into bash.

![](attachment/e837c2c2df6a63f8468cfee2a486e6ef.png)
Wait root directly?? Not possible...

![](attachment/5d301cf4b6cf678fbc8bcfbabfe3fbfb.png)
So went to home directory, found a user, entered user's home directory and got the user flag.

![](attachment/3ebbc23ab03f8b740a3762cc03d21352.png)
Went to /root directory and there was no root flag...

![](attachment/3ecbde31bf5ccd0d18a0c16ed17d3f80.png)
So went to the /backend were i was reverse shell'd and found a Dockerfile. OK! Point to be noted.

![](attachment/d82620457e08fbbbacf51b510d1157d3.png)
So, saw all the listings of the / directory and found a .dockerenv file.

![](attachment/4217a706d365eeff18f2d88ef181a86d.png)
Oh!!! So we are in a container.

![](attachment/2eebccad9d1230fb35eafefd618f0440.png)
But can see /home/augustus directory of the user how?? So, used mount command and came to know that it is mounted from the system to the container in here, which means changes in it will also affect the user's home directory that is in the system as well. Hmmm!!!! looks interesting...

![](attachment/9ec41bebeed8044b3722c03d014ba225.png)
Saw this blog on freecodecamp.org and then saw this![](attachment/b5058cb40848c3699f46573f6c499402.png)
Why do the container has 172.19.0.2 ip address? Who has 172.19.0.1? maybe the main system... We can find this out by running a port scan on 172.19.0.1, if it shows some open ports then it will be confirmed else, will go for any other way.

![](attachment/fb543f73f82e6d5b72fbcc0d486e5136.png)
nmap is not present in the docker container. Let's search for a one liner port scanning script in bash.

![](attachment/0b22cc51da99ad10784074043a5b6664.png)
Found it!!! Let's optimize the script according to the need and run it.

![](attachment/b28dfc23f92fde5ee1b9f5510497f788.png)
Port 22 of 172.19.0.1 is open.

![](attachment/0c00139548f2bb80e938167394038bb6.png)
used the same password to login as the user.

![](attachment/b3783989e7d46171a1dd3303690f1e24.png)
Logged in as the user.

So it means if add a bash shell in the user's directory, change it's permissions after going inside the container and then execute it after doing ssh as the user again will give me a root shell.

![](attachment/1ae9af427f98e22f5a57faafd9b1dc48.png)
copied binary of bash in user's home directory.

![](attachment/b50b8f1cb404bb3e55e7a4e405e9605d.png)
Saw the binary in the container.

![](attachment/c2951ffee67b8de7de479ddd3e875b98.png)
Changed the user and group of the binary and also gave rwx permissions to all three with SUID in the CONTAINER.

![](attachment/1849f2f98f92887fc3a3d510d62ecce9.png)
ssh'd again in the host system from the container and found out the permissions of bash binary is root:root with SUID.

![](attachment/1a2d6aeaafa7c2cc42b55cdd18077b08.png)
So ran it with interactive and privilege mode and got root.

![](attachment/9b8adebac8292b9f855f63bc4f48747e.png)
got root flag...