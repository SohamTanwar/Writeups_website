**ip of the machine :- 10.129.231.125**

![](attachment/eb8b795f54482e1ef7efe209c87305f0.png)
machine is on!!!

![](attachment/71c6ea57574b5ddc5630ff400dac949e.png)
Got usual ports open!!!

![](attachment/7b37935ce10f239f85b0304c785d45a1.png)
aggressive nmap scan revealed version of the services running on above found open ports.

![](attachment/0560505e39035e3219ac141fc698b8f8.png)
http and https was hosting the same stuff...

![](attachment/776f53339bced1a15e619719d0dfdf9a.png)
got some directories using ffuf...

![](attachment/dd3b24aaf134b5f6ec52b60db90fef37.png)
got a decoding web page....

![](attachment/d950b9fa21f155f0616ec3b30f1bd027.png)
also got an encoding web page....

![](attachment/e076de4ef7b4524502860e504de206f5.png)
Looks like base64 encoder to me.... Although captured this request...

![](attachment/e338ce5efb5a5c44e083b14e7fb352e5.png)
It is passing text as the parameter in data of the POST request, so let's try for command injection.

![](attachment/97fcc005c8e742973a42a93b17488485.png)
didn't work in any case and same with the decoding web page...

![](attachment/263db1389578c6d45ccad89207d5f908.png)
in dev directory got some interesting stuff...

![](attachment/9c7899a1d4636a9f792700ba984f72d2.png)
Saw notes.txt file first and just a normal to do list...

![](attachment/213c7ca0e4a297bd931c2575fe3090a7.png)
saw hype_key file and seems like hex to me...

![](attachment/329f5cb0972cb1e697e1106c4b5f2b46.png)
seems like an ssh private key!!!

![](attachment/e2614b63d0f671e2c241508b2916f36e.png)
got a private ssh key!!!

![](attachment/78124d2fec7bf69dcaf4e5ee327816c1.png)
So after looking on different web pages and directories and also looking if the web server running is vulnerable or not but still didn't find anything and then ran the "vuln" script by nmap...

![](attachment/0c5a05286fb02787648463b53630eb44.png)
Found the web application to be vulnerable with "Heartbleed" bug which is an error in openssl cryptographic library which can leak the info. which is supposed to be protected by SSL/TLS enryption...

![](attachment/b0ff04f0c18f63759fc7dbf84630e42e.png)
So searched for any possible exploits and found one, let's try it!!!

![](attachment/1e837555b8f9d2d33dc2d30dad63d07b.png)
Run the exploit with python2 as it will not work with python3. 

![](attachment/8a976d879ded78ec4816cef36c8dad38.png)
After running the exploit the leaked info. from the web server will be in the out.txt file.

![](attachment/ffea6c5dabb769d36c3092d983513c40.png)
It's a hexdump, to reverse it to get the original data whose hexdump it is, will be using xxd...

![](attachment/6302eddaf57e7c9fae118782a3fc1578.png)
Got an unusual base64 string!!! Let's decode it...

![](attachment/3bf4887fbd857b47d1153be9828f4746.png)
Seems like some random text...

So after no such vulnerabilities and stuff thought of login through ssh.

![](attachment/cd1d7f0e991b1de2171a33fdb99719d1.png)
Though of username as hype as the file name was hype and the random string that was base64 also had "hype", so tried is as the username and it worked. So, now will be adding password as the random string now...

![](attachment/c30001d22bce3b8fd102a9a822be74b7.png)
got a no mutual signature supported error...

![](attachment/e16008ecbef1deb66d1d53fd840f5f7a.png)
After spending a lot of time figuring out the error added some more options and flags and it fixed the error because current ssh commands actually don't support rsa private keys by default so had to add more options and commands...

![](attachment/15bf13070dd334f3efc561e117d5b22e.png)
got first flag...

![](attachment/61a466e736c6204b550b0025f064913b.png)
we can see .bash_history file of the user...

![](attachment/293ef4a25ba57e98c48919ac69887e9e.png)
Hmmm some tmux commands and sudo -l didn't work as password of the user is not known and also found a .tmux_conf file in user's home directory, this means that user currently logged in as might be running a tmux session.

![](attachment/8454bf8a43081cd279fede0a38336a9b.png)
yup!!!

![](attachment/70dd4db3ca605f7026ae59c7c61acb75.png)
got this random blog on tmux session hijacking on medium with some commands of tmux. So, I tried the command to open the session running.

![](attachment/e4772de86b965217e5206af56704728f.png)
So after running the command, i noticed the tmux session was running as root user and got the root flag...