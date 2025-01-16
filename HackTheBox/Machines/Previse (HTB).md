**ip of the machine :- 10.129.95.185**

![](attachment/250b3a12c8d4486807b324f7b2ebed76.png)
machine is on!!!

![](attachment/a6d43dfedd8507990d057067c809cddb.png)
Got two open ports 22 and 80.

![](attachment/0a4f759a4d6237176a889ae41f1cdf44.png)
Did an aggressive scan and found versions of all the services running on the ports.

![](attachment/44ea3de17d41ae590c712120c8b580e3.png)
Directly redirected to a php web page after entering ip address in the browser and didn't find anything in the source code, just a bunch of .css and .js files.

![](attachment/b41b269e4f0d277b45f0e237786ed780.png)
Got some directories but none of them is important as such...

![](attachment/31ae9b8a3419a7ea74f4c02578a82038.png)
Did common php file names fuzzing in the directories of the server and found one. Came up with this fuzzing because it by default redirected to login.php web page when entered in the browser.

Now every page was redirecting to login.php except....
![](attachment/c17a67981560406f836806fa489ca715.png)
nav.php which had a lot of options to explore...
Now out of these account.php or ACCOUNTS seems interesting as we can create a account and atleast login but it is also redirecting to login.php.

![](attachment/2cea3fb347be2236e2087ec51944ad26.png)
So captured the request on Burp Suite.

![](attachment/67b676aa4086b309efa8d30c5dacbd3a.png)
I sent to repeater and found a 302 as usual to login.php but....
![](attachment/2d4dc305c4d225592eb6189f4f2da39d.png)
i saw this section in the request and it seems it consists of a create account page...

![](attachment/1ffe5c37be0caaac8d38cbc33cd9c64f.png)
So first i intercepted the request which will redirect and then right click on the request > do capture > capture response to also capture the response to this request.

![](attachment/543364d4768bea0b4fdb2dab0cca08fa.png)
After capturing the response we can see 302 again.... Let's change it shall we?

![](attachment/4961d082156bc8adba8ec0a45a44fcfb.png)
change 302 to 200 and Found to ok and then forward it.

![](attachment/c9a17408362cbdffd7d45be61747f670.png)
After forward we can see we have got create account page thus successfully bypassing 302 redirection. This vulnerability is known as EAR (Execution after Redirection).
![](attachment/f3496a48bf704c779f3e99173039f373.png)
In this type of vulnerability, the redirects are ignored and sensitive pages only authenticated users can access are accessed.

![](attachment/fa5fb02d1722522801674458afa2b77a.png)
So created a test account with creds "testuser:password".

![](attachment/8145da9f640f5f28567a836a1633ec80.png)
So added that id and password and now have access to a dashboard...

![](attachment/1d310648f2b249d31fcdc1907dcc1b25.png)
In files section found a zip file by name sitebackup.zip. Let's download it and analyze it.

![](attachment/065ed597f6e840c45a2ba0ea2a4664a4.png)
Extracted and got a lot of files....

![](attachment/f7f64515dbcb49234cebe084a9a647a7.png)
Got database id and password in config.php.

![](attachment/733acf2790ce545ade558ee9689927e1.png)
logs.php file looked strange to me, it contains how we can install logs from the dashboard with a delimiter, and it is using exec() funtion of php which is used to execute os commands in linux and it is executing a log_process with python and backend and is also taking an input by name "delim" a delimiter probably.

![](attachment/41603d4f3f018cb083c459788d849a46.png)
Found the web page.....
Was write a delimiter.

![](attachment/9b0ac23a6978642869f7225b5f9a0cfc.png)
So it gave us a log file with comma as delimiter and no use of this file as such.....

Let's capture the request of this web page in burp suite and see if we can send os commands with comma can we actually get reverse shell to the web server.

![](attachment/c160711427a4ba1cd437e481fc849d54.png)
So the request is passing delim, as a parameter. Let's see if we can execute any os commands, let's try with id.

![](attachment/7489dd86b906f050d2b39fe5dffdc957.png)
Didn't show any error, let's try with sleep probably.

![](attachment/93694714d858062dd00a2f0110cbeb1f.png)
So i typed "sleep 5" which means it will get stopped for 5 seconds and got no error and more than 5 seconds, let's try to add reverse shell now.

![](attachment/a31f340a51a7fbdf86e85e99b9e98157.png)
url encoded shell along with comma and ; to get a reverse shell.

![](attachment/4d0f3c1c010ee1fbfde3920f3c29d433.png)
Now let's try to access the database first which we found in config.php file.

![](attachment/14e7ae2b888783142ed533b3d8463792.png)
wooh!!! Let's see what they have got in the database.

![](attachment/6aa15cbe9a9b525ff3e8c94d511eb435.png)
In previse database, in accounts table found a user m4lwhere and password hash of the user.

![](attachment/0cc503101ee71b102801d81bb84af8eb.png)
So added hash in a file and tried to crack it randomly with john and found the format to be md5crypt-long. Let's try cracking it again with password list and format specification this time.

![](attachment/26423e7c3ce160054277e9ea5cba2398.png)
Found the password for the user....

Let's login as user m4lwhere through ssh.

![](attachment/c83d935c1c2ca2c97e3a654e084be796.png)
Logged in as the user and also got first flag.....

![](attachment/7a80163c3ba5cbef428979f55aeb3ad7.png)
So user can only run one script in /opt directory as root user. Let's look at it what is it??

![](attachment/fa907d2bc272cb3e92a9444e7671dfd3.png)
Took some time to notice but then noticed that wit is not mentioned which gzip binary it is using/calling in the script and the answer is relative, it depends from where we are calling the script. So, will try with setting /tmp as path variable and do further.....
![](attachment/63307855afe6d7f7d6359d25cdcfe935.png)
![](attachment/3e19f9b385c2b8cb0a88c3e7399ff53d.png)
So added /tmp in path variable...

![](attachment/a810bf41aa9498f9b65d7f52413a8027.png)
Added a shell in gzip with SUID permissions.

![](attachment/9d7984443f141e508aa223864068a154.png)
made gzip executable and then ran the script with elevated permissions...

![](attachment/384f917fcae639df1bb38cf0a9f33bdc.png)
Got a shell with name bash..... So it happened because when script is executed with elevated permissions, it will not look in /usr/bin or /bin/ path for gzip executable but in /tmp directory because we set it that and then in out gzip executable we added a bash shell or root shell with SUID permissions with a copy in /tmp directory.

![](attachment/150b9f53dc50c6e93b4aff6d003a9a23.png)
So executed bash shell with elevated privileges and got our last flag...