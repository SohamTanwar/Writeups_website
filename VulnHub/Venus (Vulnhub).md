**ip of the machine :- 192.168.122.68**

![](attachment/ba8ec905d74071b8aca4e1b9bda9a952.png)
machine is on!!!

![](attachment/e21f848861e0ee6f8fa794f936b7eb8f.png)
got some open ports!!!

![](attachment/989459fab46102d46f352f722d937d7b.png)
So, got a login page first when entered the web application and it had also had creds. written as guest:guest, so , entered and now in.

![](attachment/edf1849d37f400ef2946f106a7a40a00.png)
ON directory fuzzing, found /admin directory.

![](attachment/33be7c81e7413f82ed89d93aecee1c82.png)
It redirected to a login page. So this django admin page doesn't has any default creds. Let's try if SQL injection is possible with username admin or not.

![](attachment/6938675bc70cccb605e0964090019937.png)
Got the request. But SQL injection is not possible. But recognised the cookie which is base64.

![](attachment/9fc48f03785acfb8f54bf45e7caee430.png)
But got some creds. that didn't work anywhere.

![](attachment/b8acff2a53f3a660678f40702e6485b7.png)
So, tried admin:admin and got invalid password. So, after figuring out i came to know that password is done ROT13 and then guest:thrfg is encoded to base64 in order to came up with an auth cookie.

So, let's brute force to search for possible usernames. So, will be using hydra for this purpose.

![](attachment/472b94a9119d3f3000654fa4fac88544.png)
So, got two usernames. Let's try to craft our own cookie.

![](attachment/b2851526c4f2408ad0f03e7d69ff23ed.png)
Let's change from guest to venus.

![](attachment/45e3ba6b505daa299fd736ad362c30da.png)
Let's try adding this auth cookie.

![](attachment/890d7ba7fe7821c57693beae09bcf63e.png)
In response, got a different base64 cookie.

![](attachment/bc6b5d2a0205e659a8efb17ed4ece6d7.png)
Venus and the password we didn't supply.

![](attachment/54aba5bc3b9f24b6f8f78bac2b6c872a.png)
As we know password was first ROT13d then base64 so ROT13d the password again and found that we when we supplied wrong cookie in auth (right username, wrong password), it returned right auth cookie (right username, right password).

![](attachment/633d1979091fed2b13658824c2bf1e97.png)
So, let's try this auth cookie now.

![](attachment/3beed91c0671efc8cf2499d93acb8817.png)
Got another base64 auth cookie. Let's decode it.

![](attachment/1dc3afa1b72fd5f92e84849e82ff2af0.png)
Got ROT13 password again.

![](attachment/43504f67fa7dcf7edeb499a979c7caf9.png)
Got the password. Let's try to login through ssh and if failed then will try creds. on  django admin login page.

![](attachment/45991b8072eafece380659eb385b79c3.png)
So, creds. worked and got initial access to the server.

![](attachment/973002bdfc04c4413740ab81bc511cf4.png)
Got user flag.

![](attachment/6e58eee14105d7e4a592078de7f738f9.png)
So, after manual enumeration didn't find anything, so, using linpeas to find anything for vertical priv. esc.

![](attachment/ea127d0159ae1146639aad992c913b12.png)
So, in Linux exploit suggester tab found some cves let's try their exploit for priv. esc.

![](attachment/fc6051ba8ac27bfe1259baa557c5aca1.png)
So, first showed error.

![](attachment/217349480d70a7bb059952d1746d32c0.png)
So, this exploit worked for me.

![](attachment/e5096bb0a3b4cccec8cfd706ff33330e.png)
Simply downloaded the zip in compromised machine and then ran the exploit.

![](attachment/bae2b4bd738c732a187e66a2cf069ada.png)
Got the root flag.