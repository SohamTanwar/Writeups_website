**ip address of the machine :- 10.10.143.140**

![](attachment/c19f5cb1c7e5d23d0f3c0af055da7e77.png)
First, tried to ping the machine to see whether up or not.

![](attachment/1762c642e6632ee6cc7167fc9e2a49a4.png)
Did an all port scan and found three ports.

![](attachment/396c11571c300b8432d1c15d419455b2.png)
Did a script scan and didn't find anything interesting.

![](attachment/b44d407a4c796ae6bc5eeac04beb99b7.png)
went on website/web server content machine is hosting.

![](attachment/a37dcad7a81bd8ffe871d527ed509c37.png)
![](attachment/31f59ba870f6108f3366cf8a690fd0e1.png)
Used gobuster for directory fuzzing and found a lot of directories. Now let's start looking at these directories and see what we can find.

/0 first to see what we can find.
![](attachment/984d70641607ae5dcfe0aafcd97f75f4.png)
we can see that it is running php which has a lot of vulnerabilities.

![](attachment/0dd88cee6c19b9913a4ee976e12a798c.png)
got an xml file form /0 web page and it is mentioning the version of wordpress which is helpful and another possible directory which is the same as /o itself.

![](attachment/f9fbd947356644349d1d8202f8ad4bf5.png)
/image doesn't gave anything interesting.

![](attachment/db99c97d04e9552c66c7c45434728414.png)
in /wp-admin found this login page.

![](attachment/dac85635a81da78c56d67fbd2bad75e2.png)
getting this by visiting most of the web pages.

![](attachment/e4c7517309f85d98f7c0af71a9101f41.png)
got something in /robots and a possible file name "key-1-of-3.txt".

![](attachment/53bfaca8a2ebc861cd2c777ba778dbf7.png)
found this in /sitemap.

rest didn't find anything interesting.
![](attachment/72d00908e812ca1f7ec06748e30fb8f3.png)
got a file in /robots directory and thought of seeing it and got first flag.

![](attachment/cf539e16502ae9a5d249f114b0200824.png)
as machine was using wordpress so thought of using wpscan to find something.

![](attachment/cb280458334fd83dd3e3904007247a70.png)
it also said that version that is running is outdated which we already found.

![](attachment/c59c18c530f67838451d52c70df64a65.png)
in some other file, also found this hierarchy.

Now let's see if any exploit is available to get a reverse shell or something.
![](attachment/4224158c8b51d8fa0ad0967c422e4919.png)
found possible username as "elliot" let's see if we can find password.

Also found another file in /robots.txt which is fsocity.dic which is a dictionary file.
And **By the way restarted the machine so got a new ip :- 10.10.250.120**

![](attachment/ddafde0e098a56f6e11c900c52273cf0.png)
wget this license file and will get base64 and then decode it.
possible username and password.
elliot:ER28-0652

after logging we will see all the inboxes and editor tabs to see if we can take reverse shell or not.
![](attachment/900db6ae344b39e7d8efbb9e2d25bc40.png)
so we got it added a php reverse shell script by pentestmonkey in archive.php and it can be accessed through a url which we found when applied wpscan which will help us to give the url to visit to get reverse shell.

![](attachment/ab7676b8dfa617ef46ba99249cf3394c.png)

Didn't find any useful information in Network info, cronjobs and mysql after running priv esc script.
![](attachment/357fc72e40931896830208a60b0ed627.png)
only root is running the default shell as bash.
![](attachment/48e1db021e6774a955ba4a4a413b701e.png)
Got some kernel and system info.

![](attachment/d7c212865ed76f4ce452c816d2990876.png)
![](attachment/e3a4fd2ee64a6d9b00fb8c3f8144cc08.png)
nmap was running old version so gone to GTFObins so searched and got interactive and got 3rd flag.