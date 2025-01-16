**ip of the machine :- 10.10.176.228**

![](attachment/2e5d49389a3e157242037cc996828d7c.png)
machine is on!!!

![](attachment/8f9ce22a52e91efa45fb298f3e7fbe7c.png)
got some open ports. Let's go for aggressive scan and let's see what we can find.

![](attachment/d022185c7df100b73cf2599f988a9061.png)
with aggressive scan got some info. We can see Ubuntu is running with apache web server.

![](attachment/e9153ab3753417300c5ab8174bd1a07f.png)
I visited the website with this ip and found this. Again nothing interesting.

![](attachment/d502b19eb5ec01ab77a3224bd1c7705e.png)
So thought of doing directory fuzzing as web server is what we have, and found /app directory.

![](attachment/441a706239228c9f4ab85015677b777b.png)
Before Doing Further directory fuzzing, went to /app and found pluck-4.7.13/.

![](attachment/15de37a73ac86b095ff73578240a1740.png)
after clicking on pluck to see what is in the directory, was redirected to a page named "dreaming". But got a possible version of pluck "4.7.13".

So basically was confuse what pluck is so, went on to search for it.....
![](attachment/dabf9e85296a023acb3fd3ef893854db.png)
So it is a CMS in php. Huh!!!. Which means vulnerable i guess??

![](attachment/255ef82af13aa6117a990bede0d5de03.png)
So there was a link to login as admin, so was redirected to at this page. Haven't found any password, so let's try the most obvious ones, "password", "admin" and if these two don't work then will brute force it.

![](attachment/0f103bce379f5c6dccf6d13cc2c93177.png)
was able to login through "password" as the password.

![](attachment/99abe5f0fbbcc0724f4296c91760f1f2.png)
Yay!!! Found an exploit for gaining a revshell.

![](attachment/78118ea78e81fed4aec1e8ca852c9ee1.png)
so ran the exploit and it seems to have worked.

![](attachment/e0b83f6796a03c250a44c898a2be322b.png)
i saw the source code of the exploit and it gave us a web shell.

![](attachment/3007bf514d67e1c68540fc23825518d6.png)
got three possible usernames.

![](attachment/a8badc2a8938a346e3f01b1b1955a47a.png)
So went to home directory of user death first and found close to no permissions but can run a .py file. But unable to run this .py file. So went to /opt directory.

![](attachment/7d6d5606f699ed0f7fb9adf900033ebe.png)
got atleast access to read the src code.

![](attachment/c7a41fd248763bcd3a4438cd0ae8c3aa.png)
Seems like user death trying to access database but we cannot see the password.

![](attachment/843d8ac23896114975d7105ba3bb5d46.png)
but in test.py found a possible password.

![](attachment/a33f8594f8f0cb0b5e4c12f899210775.png)
took a revshell from web shell because some things not working in web shell.

![](attachment/39bbcddf5d89f65aee3925a8fe2a536c.png)
Was able to login as lucien because in the password that we got word "lucien" was mentioned.

![](attachment/9a1dae8e8de8d37d52534cea95a8330b.png)
got one flag.

![](attachment/134e2e4f279c0421be3c59a1b4f36447.png)
so .bash_history file was readable so went through it and found mysql creds for user lucien.

![](attachment/123aa2f7b548076f3b966116807cdc48.png)
also saw what permissions lucien and saw that it can run the .py file that i saw in the home directory of death but can be run as user death.

![](attachment/18b422167b960cad251d47959458cf54.png)
also saw .mysql_history which seems a bit obfuscated but after understanding it manually, i think some records are changed in library database and further dreams table.

![](attachment/7c05913ea8506ee8d786ac39bea68562.png)
was able to login as user lucien in mysql server.

![](attachment/257c592fe02cf03751bc8a53c2f91b66.png)
got password hash for death but was unable to crack it.

So saw the .py file again that user death can execute and there found a line where it is executing the query. It means if we add a shell in the table which will be executed as user "death" and we will get a bash shell running as user death.
![](attachment/63d6c896cf802efbf29b33d9bbe4eebd.png)
so it basically taking each query and executing it using the python program.

![](attachment/5e37460375fc9733d143221d212739dd.png)
so tried to add a bash shell in it. As user lucien is allowed to run only that .py as user death, we will get a shell as user "death".

![](attachment/824d19b1561a16f12d0779ac697a1651.png)
got the shell but cannot perform any operations, or basically no commands are working...

![](attachment/98358810814d7cc460e755ce042ae53f.png)
so chmod 777 to the script and then exited out of the shell which was not working.

![](attachment/95630cf890f704c2ab600348eccfe528.png)
now we can see the contents and even the password.

![](attachment/0cf820e04ab595cd00614f55735c12ca.png)
So was able to login as user death in mysql database but don't know what to do so i exitted out of the mysql.

![](attachment/25bd9c198c1e93b3e4ce4d3a02502f8f.png)
So did some password spraying whether user "death" is using the same password for his account and was right.

![](attachment/6f31f6dbd250124801c5ad3885f96bfb.png)
got second flag....

![](attachment/fa90307e78b10b55222f3106dfe479ea.png)
so user death cannot run nothing as another user or root.

![](attachment/482514cc6c9da96a3e221af127047f5f.png)
So tried to enter command "find / -group death -type f 2>/dev/null" and most of the results were from /.local/lib/python3.8, so will check that directory manually right now. But didn't find anything then i redirected the output of the command in a file and then found a file with suspicious name.

![](attachment/3745d2fe1fa0f3a27774ec18b1583be3.png)
shutil.py!!!

![](attachment/05d8b94fc8be4f4e8c5cbcce94e3a513.png)
we can write in this file.

![](attachment/7244f6f6dbf2c03644c48fb81ab9dbab.png)
added a rev shell in the file.

![](attachment/551398951a7e5d120f2038bbe04c6c55.png)
got the last flag....