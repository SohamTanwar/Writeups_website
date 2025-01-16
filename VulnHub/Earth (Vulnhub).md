**ip of the machine :- 192.168.122.84**

![](attachment/0ee4b857201079bcd59a46b486e0a382.png)
machine is on!!!

![](attachment/f4c42d4ee42b448c322d8c4c6829b874.png)
Got three open ports this time.

![](attachment/953a326d155c23e2eb56a0f64d431adc.png)
Did an aggressive scan and found about the versions of the services running on the ports.

![](attachment/9cdad9990f134b728523e82f8793000c.png)
Nothing on port 80 web server. Will do directory fuzzing after checking the one on port 443.

![](attachment/a15719776c7fa0da7d233163edd68b22.png)
Just the default page of the fedora web server.

![](attachment/f646a038b75349e6efdba68f3fb24392.png)
Found only cgi-bin.

![](attachment/faf22a96fcc919e5ce3f16aa224ce237.png)
On port 443 also some 403s.

![](attachment/5a9a422a7cc3fb4a26be80112c2601ac.png)
So, saw the SSL certificate and got a domain.

![](attachment/a73f685b07967476b5616f9b4abe3b68.png)
So, added this domain and ip in /etc/hosts file.

![](attachment/bd15a4c5c09dace10ce9889d1cf98229.png)
Went to the domain and saw the application now.

![](attachment/43ed056143f51fe4b5179a240eb10511.png)
Did directory fuzzing on earth.local and this time got an admin web page.

![](attachment/f44c3664c3ef42d4e2e0696333c2cd2f.png)
It showed an error after entering a basic SQL injection payload. But it is not vulnerable to SQL injection.

![](attachment/03a1ff391873251c061ce61667b84260.png)
So, saw the certificate in more depth in another browser and found another sub domain. Let's add this also in /etc/hosts.

![](attachment/01b77b2bd669bb73041515478fe3b245.png)
This another sub domain is also hosting same stuff. Let's do directory fuzzing on this.

![](attachment/ada417dea5099003b28bfecf230c7be0.png)
Oh!!! Found robots.txt.

![](attachment/f972a54fc27b2f7441f91a05a6298108.png)
Found a lot of file and directories but what is the last one. Let's see!!

![](attachment/1f36de83714af706b2b6f8bb39fe1ee2.png)
This file has some really good information related to admin login.

![](attachment/9c53f98fb29ffaf2503a73e7e93e4e07.png)
Got the test file, testingnotes.txt file was talking about.

![](attachment/e562e2f8be6cbe4fffcb02864516e8ce.png)
So, went to cyberchef and entered the encrypted data from home page and it looked like hex so did "from hex", then in testnotes.txt it was mentioned that it is xor and testdata file was given so added the text in testdata as the key and got some repetitive text.

![](attachment/6ae40da972ce2b79eec64c03f2b08d88.png)
So, tried adding the password with the username in the admin panel (terra:earthclimatechangebad4humans).

![](attachment/fff6591ee302008b1884249a21d8eff6.png)
Now can execute commands on the web application.

![](attachment/9c5e6d92c06eda9de711fb258ba11e12.png)
Did "id" command to test and it worked.

![](attachment/735d01324d6471bf60402a4c2d13f0e7.png)
After adding one reverse shell payload, it said remote connection are forbidden. Let's try another payload.

![](attachment/e71d1f9816f676c627e003d733a16cd8.png)
Again this also didn't work.

![](attachment/173e02d9a36d7c149cff3c3be2de2546.png)
curl one didn't work as well.

![](attachment/cdc771a7340d11a8f24b0f8950632df5.png)
So ,base64d rev shell payload.

![](attachment/7baac59986c0c3cfa8a73c2842ff529b.png)
Entered.

![](attachment/6febec1ef0e32b4c91941e920a4333a4.png)
Got it!!!

![](attachment/3c027e20e43e66f5ebe82567d8b6e3ac.png)
Found user flag in earth_web directory.

![](attachment/72949bf3e3653730146de353a2145a6b.png)
Found some SUID binaries. Let's check reset_root.

![](attachment/36dcc22a53dd2c0f433bfb97b84cea23.png)
So, using /dev/tcp got the file on my machine as the machine doesn't has python.

![](attachment/b07a3ea73d8896c6c1cf4d4a62ba862e.png)
So, did strings on this binary and found that it will change the password of root user to EARTH, but it needs something but what is not here. 

![](attachment/e07347b5dfdcdd1dbcb95ae23163c5af.png)
Let's use ltrace to see library calls so that we can see what triggers it is talking about.

![](attachment/249debbde81d46714bb1e1e8d508defb.png)
So, found three dependencies/files it is looking when executed.

![](attachment/947d69e9fe86baa2dfaf01286ea11911.png)
So, just tried the most obvious approach which is created the files and ran the binary and it worked.

![](attachment/17c7d2b892d09870cfb6072638ac4361.png)
Got root.

![](attachment/9b2a0248485b4fbf72a4d1ab49ddff94.png)