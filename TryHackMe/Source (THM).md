**ip of the machine :- 10.10.140.36**

![](attachment/1c8be2f469f360d5d50bce3ff34e06a0.png)
machine is on!!!

![](attachment/881061b2c9064b52b514e396f3849199.png)
Only 2 ports are open but what is this service running at port 10000??

![](attachment/7e694349bbb7fee57b72d0ec2bcdf550.png)
So on port 10000 at http server is running and is Webmin.

![](attachment/d41b77c4c2b65051eeac0c494bada63c.png)
So before going for directory fuzzing, though of visiting web application manually and see what's going one, what's present etc.

![](attachment/03dcbee5c2857f28ba85b988143b5509.png)
cannot view page source....

![](attachment/4ba1457734be96d5b498d1b139618499.png)no sql injection and xss possible as well. Let's look if there are any vulnerabilities that can give us RCE as we at least have the version though.

![](attachment/2867641b979918ed31c35d39c41f2508.png)
We found an exploit for unauthenticated RCE, which means we don't have to login and still we can get reverse shell to the backend server.

![](attachment/cf9de4b7edc68fd5062455ec626068d5.png)
This is the exploit, will be using...

![](attachment/8d9d9ffd61ca2b9d8e9b548ce1985059.png)
Let's use it with the help of provided example.

![](attachment/9018cb27e35d12013732a842a2b0e300.png)
So ran it according to the given example provided by the exploit and got the id of root user. Now instead of id let's add reverse shell...

![](attachment/c17e6b02be00a35f64e7cfdf79872462.png)
was unable to take a reverse shell through above exploit in python so will be using metasploit and found the exploit which no. 10. A backdoor for password change, which is what i looked in the above python exploit, so will be using that.

![](attachment/b13f9819d642b7d2ae724a5b105f7895.png)
set all the options and enter exploit.

![](attachment/9b178102a1988c66c68c87a22cfac3e2.png)
got reverse shell let's upgrade the shell.

![](attachment/e9de083239d3363acfda215b9260dcda.png)
Directly logged in as root user after getting reverse shell.

![](attachment/0af8aa89c483f72a4b80abdb3d49c058.png)
got our first flag...

![](attachment/0e724a8b6c6d898ba5a88119fc194770.png)
got our second/last flag...