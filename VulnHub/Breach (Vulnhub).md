ip address of the machine 192.168.110.140/24

**Enumeration** (nmap)
![](attachment/8c9bcc3b23e40c1e03c3b76f8c348b36.png)
First we did a nmap ping scan also known as ping scan or ping sweep (-sn) to see whether the host is up or not.
![](attachment/9a5cceb71e2963679dc7685c7511c3ef.png)
Now, we saw that host is up so we used  -Pn to not ping the host and directly scanning all the ports by using (-p-) and -T5 to speed up the process and using --max-rate=10000 to further speed up the process by sending 10000 packets per second and -o is for the output file. 
So, basically we can see that all the ports are open literally all 65535 ports which is highly unlikely and unusual.
Now, having these many ports being open is close to impossible so may be a firewall or any security mechanism is enforced which is giving us incorrect results so we have to do an  xmas which will send a malformed package and want to receive RST flag in response of this malformed request.
![](attachment/c020f8c0aa7d42e673e8b8b8b452dff9.png)
So after doing xmas scan we received that three ports are open and filtered means that we can expect a firewall to act or perform on these ports.
Now after finding open ports we will go for version scanning on these ports to understand more about the services running on these ports.
![](attachment/4096423de0499ab309bae19df39835ad.png)
So after running version scanning (-sV) we can see that at port 80 HTTP server is running and operating system is ubuntu.
![](attachment/7252ff3c9025dea25d6f649fdd62bd2a.png)
Now to get more further in-depth scanning can be done using -A which runs three types of scans (traceroute, version scanning, os detection) and get more verbose information.

**Directory Fuzzing** (gobuster)
So we noticed that it is running http on port 80 and that to an apache in ubuntu so lets go to http://192.168.110.140.
![](attachment/a302c030c62821f1afb37fa195cbbd58.png)
So there must be some directories in the web server where we can find further things for exploitation so now will be doing directory fuzzing using "gobuster".
![](attachment/ff633a3b78928abdb25a355a0244ab0f.png)
So, while doing directory fuzzing we found many directories with status codes and here, in this command -w stands for wordlist and "dir" for finding directories with an associated url (-u). 
So here, we can see that if there is a 400 status code we cannot access them which means we have to further inspect 200 and 300 status codes ones which are .gitignore, images and index.html.

**Vulnerability Scanning** (nikto)
"nikto" is a tool that can be used to scan web server for known vulnerabilities.
![](attachment/8d81e1fca7b2f34ee41be5627ce61e86.png)
So here we have used nikto on the machine and creating an output file using (-o)
![](attachment/00af187129ecb65ee583533c26f48bc7.png)
So nikto revealed this information, and here we can see that **apache server machine is running is outdated**. We also found **.gitignore** which contains the directory structure of the machine (web server) and **/#wp-config.php#** file which contains credentials. We can also see **/icons/README file** which is the apache default file.
.gitignore file
![](attachment/42d6cfee64904c196063dad823bc644e.png)
icons/README file
![](attachment/f54feb2c0891593ad527491850b9ce7a.png)
Unable to access the config file directly through url modification.

**Web app Enumeration**
After manual web app inspection we found about two users and a little backstory on the web page. (Bill Lumbergh and Peter GIbbons)
![](attachment/dba617fd3c1cd1a27ee76a0925dca5fe.png)
now let's again visit /images directory and try to look at each image.
![](attachment/8a3da9c153a9be57538ef233d99c59e3.png)
Only first image was of some use and it hinted to look at the source code of the website at home page.
![](attachment/6a89acc580435119aaa489a018515c01.png)
Now after seeing source code we can see that we found a link to **initech website** just by clicking on the image on the home page.
![](attachment/0321a21d94cdc7b94688938dd970d5c6.png)
In source code, also found this base64 string which means something so will be decoding it on cyberchef. It was a double encoded base64.
![](attachment/d7570b640ba02b74c5119801c01d4049.png)
so here after using cyberchef, found some credentials.
( pgibbons : damnitfeel$goodtobeagang $ta )
( username : passwords )
So now let's visit another website which was "initech.html" and see what we can find there.
![](attachment/bd57b66955d16210b8653a0f291ea427.png)
First we will see the source code and see what we can find and we found nothing. So here, home page, cake and stapler are those images we saw in images directory but now the employee portal is something new so we will inspect that.
![](attachment/f590069081093d9bf173066e99250133.png)
We have to enter some credentials, so let's try entering the one we found.
![](attachment/5334d5af606d7c1dcf5d575c722174ff.png)
After entering found credentials we were able to enter into peter gibbons account. 
So now we will be clicking everywhere to see what we can find.
![](attachment/6c80328cea51a149e4313f3374ae9b68.png)
After clicking on inbox we found some mails in it. Now will be inspecting the mails further.
![](attachment/3a16a3ddc4ae72dac0d8d5fe9c4e968c.png)
at last third mail found a really interesting file. ( 192.168.110.140/.keystore ) and we also find another possible username : admin@breach.local
![](attachment/131f8d538807a717ed640aee0b175c26.png)
After visiting this url we downloaded this file.
Now further exploring more options further.
So in banners tab fond this directory.
![](attachment/f1c8ccac2405c878c898a8d355ae7f8a.png)
In search tab we found that we can search for members of the company.
![](attachment/a325a4e297e0bf260f273102a23cfee9.png)
In edit account option we were able to find more about our logged in user.
![](attachment/7be06b798201b9100f326ae04d31aeff.png)
Now let's explore search tab that is given.
![](attachment/bd13bd88e47110c3be19750db4645fb7.png)
So after entering bill or admin we found nothing but after entering "peter" which is we are logged in as, we found a .pcap file and some more information which is "alias, storepassword, keypassword are all set to 'tomcat' ".

**Analysing the files and further accessing webpages** (.pcap and keystore)
Now first we saw what type of file keystore is and we found out it is a "java keystore" file which is used to store digital certificates.
![](attachment/9e6e8b19408cabde0a7ddaa821f405ad.png)
On some browser searches also came to know that this file is also used to store corresponding public and private key pairs and is used in TLS connection.
![](attachment/f335be90d5d03be009511053b80bb95a.png)
Also a tool was also being seen which is a certificate and key management utility.
Will be using this tool to export the certificate from the **keystore file** and then will be adding this certificate into the wireshark to decrypt the HTTPS ( TLS ) traffic. 
![](attachment/955b3d42670ef08660d0847f4bc35819.png)
We knew about ' tomcat ' when we were inspecting the mails in inbox. 
![](attachment/0b8192e256cfd2e16105efbc4ac9a060.png)
When we tried to add the certificate into wireshark we got this error which means that certificate should be in format of PKCS12 and not x.509.
![](attachment/19fef8acb5c2f8795620dc6b4f2ac37a.png)
Did some browser searches and came to know that file of pkcs12 is .p12.
So, will be using "keytool" to generate a certificate in pkcs12 format.
![](attachment/5a2b47fe77ea83ba2982d23cae0a3543.png)
Now after importing certificate in edit -> preferences -> protocol -> TLS -> RSA keys
Now we have imported for TLS protocol so we will be able to follow TLS stream only and not TCP.
![](attachment/10a078196b17937b402dec9a0abc179c.png)
Now we will notice that we have successfully bypassed SSL/TLS handshake conversations between client and server after importing the certificate.
![](attachment/dfc3abb73d93eeec17cfb6ce3938b54a.png)
Found this authorisation header in one of the get request which was giving 200 status code.
Also found some other credentials as well which was giving 401 status so didn't though of it.
Let's see if this encoded string might contain something....
![](attachment/6dba486c9e6aefec69ddd49ce967204d.png)
got some creds. of the tomcat account.
![](attachment/8f3883bb626838c206b8c4477037a979.png)
the request was made at this url with 8443 port which has HTTPS connection for which we didin't get any information.
![](attachment/143a89155a9bb233b44ace879ef218d7.png)
So when we add the url with https and at the port 8443 it comes with a pop up with username and password which we already found which was of tomcat.
![](attachment/54d1c32d21a0f5ce86640c947fadc7d3.png)
Just after adding credentials we landed to the tomcat page of the web application.
                            OR
Another way of accessing the above webpage using burpsuite by adding client TLS certificate to burpsuite ......
We can add client certificate that we got manually by going to settings -> network -> TLS -> client TLS certificates
![](attachment/2ec4f2dae9bc0d2bf7a8d37a0d473ce8.png)
![](attachment/69eae189ca8fd8f4806af4c8c3b91cde.png)
Remember that if we add client TLS certificate to the burp settings and then use burp proxy in browser then we can directly open by entering ip:port/where_we_want_to_go but if we don't user client TLS certificate then we have to type https://ip:port/where_we_want_to_go.
Basically we have to add extra https:// to access the above web page if we don't use burpsuite.
![](attachment/b392eaa2703310e2eb738dcd5ca7e6f1.png)
After exploring the tomcat webpage we saw a .war file upload box and we also saw a bit versioning of the tomcat server.

**Gaining Access**
Now that we know the version of tomcat we can use "searchsploit" to actually search for exploits for this version of apache tomcat.
![](attachment/5713d4ecae593730a463a5da5e4fc622.png)
'-v' in grep means we need the searches that does not have metasploit in them.
So after trying to find exploit and narrowing down searches we didn't find any exploits for this version of tomcat.
Now, we also saw a WAR file upload column, maybe it can be used for file upload vulnerability kind of attack to get remote access.
So in order to upload we have to understand more about the war files.
![](attachment/d3baf4385bfed5a7eeb3b5041638faed.png)
So basically it consists of a large number of java files or is a java bundle but for web applications.
So to create payload, will be using **msfvenom**.
![](attachment/1718808c20d42e5279af38e0e9385d20.png)
so here, "-l" means list payloads and then we are grepping only the ones with java and will be using jsp_shell_reverse_tcp because "jsp" means "java server pages" so it is the most accurate one to use in this case.
![](attachment/07bd1197e30baaed60ce45eaf3f8a99c.png)
'-p' for selecting payload and LHOST is our ip address on which we will receive and LPORT is our port at which we will receive connection when we will fire up netcat in listen mode. '-f' is for the format and we are directing that payload in a file with .war extension as we can only upload .war file.
![](attachment/292f70212a5cc7db72e9a1bab9b503ed.png)
'-l' means we are listening and waiting for connection to happen at this port, '-n' means numeric only (only ip address no domain), '-v' is for verbosity and '-p' is for the port we are specifying which is 9999 in this case.
![](attachment/ed3aecedecf44177037ce3ef30b18302.png)
Here, we can see after uploading the file, we got connection this means now we can execute commands.
![](attachment/db935baa19b11754e6b3bce0034428fe.png)
So here, using pty we were able to make it a little bit more understandable and interactive. "-c" option in python means that a **cmd command as string** can be directly executed in terminal in literally one line.

**Horizontal Privilege Escalation**
So now we will try to login as other users and not root user to enumerate further and get some more information.
![](attachment/a8f73a63325f28d7bfd42cb118088d37.png)
So for this, started a local server on my machine and then will use wget in Breach to install the Privilege Escalation script.
![](attachment/99eb27e04826b49fe346703855f3b964.png)
We downloaded the script on the Breach machine.
![](attachment/cb27537be790823ed7e98628de926b58.png)
Now we got a lot of information like /etc/passwd file, SUID and SGID files etc.
After inspecting the data we got after running the script the only thing we can go for is a mysql database to get passwords for other users.
![](attachment/4627ae1d488d3ba43ba772cddd0891dd.png)
Was able to login into mysql database as root and that to without any password.
![](attachment/2dce39e2891bb4890e15f553cab68f32.png)
so now we will use impresscms database and see how many tables are there and what we can get from them.
![](attachment/a4891b8f5a5f24e3ffeeadccbe38ed75.png)
So after seeing all the tables in impresscms database, found two tables being suspicious or possibility of having some passwords.
![](attachment/9c2b190a6c6382be994d0901fb6e9e38.png)
So first one had the password of only impresscms admin and second file even had the password of Peter Gibbons and Michael Bolton.
But these are impresscms users and there passwords and not the ones we need for privilege escalation.
So let's inspect other tables in other databases.
![](attachment/f464c3262a9c5c919b5055feeac6743f.png)
So in mysql database and user table we found a username "milton" and his encrypted password. So let's crack milton's password and may be we can do horizontal privilege escalation with it.
![](attachment/dfe2f72c13b333a524eddf05c9b7fed3.png)
we were able to crack the hash and the password is "thelaststraw".
![](attachment/071ea249bf6003150c2e6c2c473d0c0b.png)
so with the help of password we were able to do horizontal privilege escalation and were able to login as another user "milton".
Now we can further enumerate as milton user like his home directory.
After seeing all of the files and directories we didn't find anything.
![](attachment/b28c61dd91350c7f4c23f7e627a203cb.png)
'-l' in this case means we are listing whether user milton has any root privileges or not and he has doesn't has any.

Vertical Privilege Escalation
![](attachment/fa9d47d975266c57ee715d19caf0323f.png)
These are all the users in the Machine.
After seeing all the processes. user profiling and running script to see other things as well as /etc/shadow and other files but didn't find anything interesting to escalate privileges.
![](attachment/996db5bc46741133e6b12e741267bea8.png)
We can see all the GUID and SUID bins and then search them over here to get a root shell. But in this case didn't find any.
We can same seach on searchsploit or exploitdb to find whether any binary can get us a root access or not.
Now, we logged in as tomcat, then we logged into milton's account to see if he has any privileges or not and now only bill lumbergh is left, so let's see /home directory.
![](attachment/0f0d825d3b34b7beba49d6ff192316c9.png)
so now we know that bill's username is "blumbergh" now we didn't found any way in our priv esc. script to login as bill so let's go to website to see what we can found about him.
![](attachment/d42ae60f73613899a4078d6f5b4c29a9.png)
Bill did CISSP which we came to know from the home page but it is not his password.
The mail to peter from bill doesn't contain anything interesting.
Now we can see the image of Bill in /images directory. 
![](attachment/16ca52c9115705634d4bb4d6fe1c2350.png)
Now, may be the password might be hidden inside this image or maybe in the metadata/exifdata.
![](attachment/10ee404f176f070234becfe27b4b0dad.png)
So we ran a tool named exiftool which displays exifdata of an image and in the comment section we see "coffeestains" which is unusual which might be his password.
![](attachment/6e7b974cc23d7659a32d9656c0756dfe.png)
So here we can see that bill has some root privileges to basically run a script and only one binary.
Now let's see what is inside the script.
![](attachment/4087b758c218cda3639ccfa0f0ede2f2.png)
This script is scheduled to run after every 3 minutes as root user so editing it will be helpful but using command "tee" because directly may be we cannot edit it.
![](attachment/bff8c8e9598e65608213067b715b5d32.png)
So this is the command takes an input and then output it to any file specified and bill can only modify one script so we will try to add a reverse shell command to get a reverse shell as root user as file is ran as root so reverse shell inside it will also be run as root.
![](attachment/a98eb08cedeed06d40047b3016906bf2.png)
So here, we have added the reverse shell to the script and now we have to wait for the connection.
![](attachment/d88627914d86ba5a87583851756e9b15.png)
After some time we can see that our reverse shell is connected.
![](attachment/387a2b7ff22b09b4cf5540d4b0abf737.png)
So here, we have got the flag and successfully completed the machine "Breach".
