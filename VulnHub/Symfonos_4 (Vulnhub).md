**ip of the machine :- 192.168.122.172**

![](attachment/f0e334afc55ce285811435a19137fc98.png)
machine is on!!!

![](attachment/3eee2893550fc32ee4eeaade7c95a46f.png)
Got two open ports!!!

![](attachment/847fb6fd002a32360c917828bd140bba.png)
Aggressive scan didn't reveal something interesting.

![](attachment/9826dd772e6988a4e990428570a96c3e.png)
Nothing on the website that can be found directly.

![](attachment/b81aeafd7e71aeb57f1b157ac6140bff.png)
Nothing even in the src. code.

![](attachment/9a72ba3d69ea4d5a5e282d6db8b2c21c.png)
Got some directories by directory fuzzing with ffuf.

![](attachment/ee46c0ca8233c33cbfdf8fd9602df10b.png)
So, one directory named "manual" showed us the manual for apache web server. Let's see if we can find an vulnerability or exploit associated with the current running version of the apache web server.

![](attachment/3cc6f871515cf7367d1f8a91f56fa6fc.png)
So, this time added extensions to find for and also changed the wordlist and got two .php files to look for atlantis.php and sea.php.

![](attachment/ed46d050e0abeef552b1d2d45e274554.png)
sea.php has an option to select god.

![](attachment/72ae85d258d7fe804a95c89a6b476635.png)
After selecting a god it queried in url with a parameter, so maybe LFI is possible here, let's try.

![](attachment/366037f115a5a4a6c8f4d666ce3a3b8b.png)
Nah!!! I don't think so LFI is possible here.

![](attachment/1bdb07105c06ffbbe1282fd87aeb1e9c.png)
Nah!!! Not even xss. Let's try to visit and sea what is in atlantis.php web page.

![](attachment/1a0e3eb27d1e060becfd51f4ec3c6df8.png)
A login page?

![](attachment/e58f3eb7853ebec28adf2fa00fe440bf.png)
So, added some random creds. and got nothing. ![](attachment/12e06b7c8e6591ea865d07e33b5d0dbf.png)
Just a normal POST request with 200 status code.

![](attachment/1dceebe46e3848731ff914b58650f2de.png)
So, added SQL injection payload (admin' OR 1=1;--) which is URL encoded and....
![](attachment/b7b0e58076e5b948c712d378c488dc37.png)
Got a redirection to sea.php. So, this means that this login page had a SQL injection vulnerability, so we bypassed login form by SQL injection.

![](attachment/115cdd32bd925029655ee45b7204221a.png)
So, /etc/passwd didn't work, but we know that LFI was there, so tried to see auth logs for the ssh as we also have ssh running on the machine.

![](attachment/79994f086bc800f760650e26b06171af.png)
So, went to "payload all things" and clicked on "file inclusion" category and found these. Log file is what we got or basically we can see, and we need RCE and we also have an ssh port open, so we can try the payload and see if they work or not.

![](attachment/890b786760004cb4eb5242bbe67028ee.png)
It's php only!!! Let's try it.

![](attachment/ecf215f4d93e0728e24cf526ae84379d.png)
Yeah!!! It's not working right now. Let's try to do using metasploit.

![](attachment/f3639fd8527bc8e5f550f93b4636530e.png)
It worked i guess.... Let's test it.

![](attachment/41a23d619a743e8e8efbcd90edbb07d6.png)
Wow, these are recent, so it is working. So, finally did ssh log poisoning in order to perform RCE.

![](attachment/b08b0ac99ea08e90a6ed685bbf16b10d.png)
So added url encoded reverse shell payload.

![](attachment/d19a57f9e49484e34dc3e481d53dc732.png)
Got reverse shell.

![](attachment/4fe077ec6ebacaea9683912b163c13c5.png)
Found one user in the home directory but nothing interesting.

![](attachment/2f065431d335f36d782721e2547e5fd7.png)
After finding manually in the machine for something, found some files.

![](attachment/2b30fa6c389cd9f84e8814e90f29b66c.png)
a flask code, does this mean that this server is running another application as well on any other port which is not visible to us. Let's see that.

![](attachment/822eeb2723ea2f9a0277dc6b04baf6fa.png)
So, 3306 is running mysql whose creds. are still unknown, 22 for ssh and 80 is for http. Then, what is running on port 8080 then. We can see it by port forwarding through ssh on our attacker machine. But we still need creds. for port forwarding. Let's see if we can find any creds.

![](attachment/1f69bac186b8afbd5fbea46b05080a50.png)
atlantis.php had creds. hardcoded in it because it is where we performed SQL injection, so checked here to see if we can find anything or not. Let's login into mysql through creds.

![](attachment/028339ec388dca3062d17134549f0e69.png)
I'm in...

![](attachment/443b24a7fe7e14ea344c0eb3a5d83b2d.png)
So, found some hashes but was unable to crack them.

![](attachment/3f112f59a82da26b045089ad947bcd7d.png)
So, performed password spraying out of curiosity and the password to access the database is on user poseidon as well.

![](attachment/cabca6d1d0aab24f84c5e4211b3b18f7.png)
So, logged in as poseidon through ssh and also port forwarded to my localhost 8081.

![](attachment/73cb1475594adad478068e5122bbaae3.png)
Now, that's the web page we have forwarded.

![](attachment/461883c9f9a141ecd534fc982ba9c503.png)
So, web page said cookie, so went to check it and it was base64. Let's decode it.

![](attachment/f484a7823edbbc4344c3ead9bf3ba647.png)
Ok!!! What does this mean now, let's see.

![](attachment/9e3775c65eb8635b493b82b4565a868f.png)
So, i looked at the src. code to see what i can do, i know that cookie is in the form of base64 which is understood. But what the hell is jsonpickle??

![](attachment/0045bc1dc78c0ba47b8b839adae28bff.png)
So, searched about jsonpickle and came to know that it has deserialisation vulnerability. So wrote a python script to get a base64 and exploit it.

![](attachment/173d30498c2a728fe267d373d11fdcba.png)
So, on decoding base64, it will look like this.

![](attachment/1d4ab7aa2b1bfb17f1e871b00ffb3eae.png)
So, pasted it in the place of cookie.

![](attachment/f75483af9b0cf51c961e1bc459d1f54c.png)
Ah!!! Internal server error.

![](attachment/a402b7f5d3d45c9609c8f6a3fd60c151.png)
But in temp directory got a pwn shell that i created in that script.

![](attachment/0f2e24dbf25f2dedd4922f773c1713fd.png)
Got root.

![](attachment/08ac0a19b13b55e2c0734f0e97b112cc.png)
