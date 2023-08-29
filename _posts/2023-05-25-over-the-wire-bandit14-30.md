---
layout: post
title: Over The Wire - Bandit Walkthrough Level 14-30
subtitle: Little documentation of how I completed Bandit. Part 2.
categories: linux 
tags: [linux, ctf]
banner:
  image: /assets/images/banners/code-blur.jpeg
  opacity: 0.618
  background: "#000"
  height: "70vh"
  min_height: "38vh"
  heading_style: "font-size: 3em; font-weight: bold"
  subheading_style: "color: #9580ff"
---

## Level 14-15
**Task:** The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

**Connect from user bandit13:**
```bash
ssh bandit14@localhost -i sshkey.private -p 2220
```

In the previous article, we found the password for level 14 and successfully logged in as user bandit14. Now, we need to get the password for the next level. To do this, we have to submit the current level's password to port 30000 on localhost.

To retrieve the password for the current level, we used the cat command:
```bash
cat /etc/bandit_pass/bandit14
``` 

We connect to port 30000 using: ```telnet localhost 30000``` and once connected, we enter the current password. It gets checked, and if it matches, the password for the next level is displayed on the screen.

We will use this password to establish an SSH connection as bandit15.
<br />
<br />

## Level 15-16
**Task:** The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command.<br /><br />
**Connect:** ```ssh bandit15@bandit.labs.overthewire.org -p 2220```

To accomplish this, we utilize the ```openssl``` command with the ```s_client``` parameter, which indicates that we are connecting as the client to the localhost hostname on port 30001. Additionally, we include the ```-ign_eof``` option to prevent the connection from closing when the end of the file is reached in the input.
```bash
openssl s_client -connect localhost:30001 -ign_eof
``` 
After establishing the connection, we provide it with the password for the bandit15. It is verified and after verification, the password for the next level is provided. We will use this password to get an SSH connection as bandit16.

<br />
<br />

## Level 16-17
**Task:** The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.<br /><br />
**Connect:** ```ssh bandit16@bandit.labs.overthewire.org -p 2220```

Here we can do some different things. One is to use ```nmap``` as it's one of the commands recommended in this level.
For this you could use:
```bash
nmap -A localhost -p 31000-32000
# And here are an output of what we get:

31790/tcp open  ssl/unknown # Here
| fingerprint-strings: 
|   FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SIPOptions, SSLSessionReq, TLSSessionReq, TerminalServerCookie: 
|_    Wrong! Please enter the correct current password # A message that hints that we need to enter the password on that port
| ssl-cert: Subject: commonName=localhost

``` 
Here we can see a port with openssl and it wants a password.

You could also use ```netstat```:
```bash
netstat -tulpn

# The output
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
netstat: no support for AF INET (tcp) on this system.
tcp6       0      0 :::31518                :::*                    LISTEN      -                   
tcp6       0      0 :::22                   :::*                    LISTEN      -                   
tcp6       0      0 :::2220                 :::*                    LISTEN      -                   
tcp6       0      0 :::2230                 :::*                    LISTEN      -                   
tcp6       0      0 :::2231                 :::*                    LISTEN      -                   
tcp6       0      0 :::2232                 :::*                    LISTEN      -                   
tcp6       0      0 :::31790                :::*                    LISTEN      -                   
tcp6       0      0 :::30001                :::*                    LISTEN      -                   
tcp6       0      0 :::30002                :::*                    LISTEN      -  
```
Here you will see two ports you could try. 31518 & 31790. Here you can try both. Here it is hard to know which is the correct one. You need to try both ports. So ```nmap``` is easier. But you may not have nmap installed.

Now we will connect to this port using openssl as localhost:
```bash
openssl s_client -connect localhost:31790
``` 

After connecting to the port, we will have to enter the password of bandit16. This password goes under verification. Upon a successful match, we are provided with an RSA key.

Now to use this RSA key, we need to create a private key. But we can’t do this inside the home directory as we lack necessary permissions. So, we create a directory in /tmp directory using mkdir command. On traversing to that newly created directory, we will create a private key. We can name it anything we want. Here we are using the nano editor to paste the private key.
```bash
mkdir /tmp/adminpenguin_ssh
cd /tmp/adminpenguin_ssh
nano adminpenguin.private
```

SSH won’t allow any private key with such open permissions. So, we will have to change the permissions. We will use the chmod command to apply the permissions equivalent to 600. This means that only the owner can read and write the file. We will use this private key to get an SSH connection as bandit17.
```bash
chmod 600 adminpenguin.private
ssh bandit17@localhost -i adminpenguin.private -p 2220
```
I had to use ```-p 2220``` to be able to connect. Without it I got:<br />
```!!! You are trying to log into this SSH server on port 22, which is not intended.```


<br />
<br />

## Level 17-18
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

**NOTE:** if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19.<br />

As bandit17, we log in and use 'ls' to find two files: password.new and password.old. The only difference is the changed password. By using 'diff', we uncover the required password, enabling an SSH connection as bandit18.
```bash
bandit17@bandit:~$ ls
bandit17@bandit:~$ diff passwords.old passwords.new 
42c42
< glZreTEH1V3cGKL6g4conYqZqaEj0mte
---
> hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
```





Now copy ```hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg``` and log out and connect to ```ssh bandit19@bandit.labs.overthewire.org -p 2220```


<br />
<br />

## Level 18-19
**Task:** The password for the next level is stored in the only human-readable file in the **inhere** directory. **Tip:** if your terminal is messed up, try the ```reset``` command.<br />
**Connect:** ```ssh bandit4@bandit.labs.overthewire.org -p 2220```


<br />
<br />

## Level 19-20
**Task:** The password for the next level is stored in a file somewhere under the ```inhere``` directory and has all of the following properties:

* human-readable
* 1033 bytes in size
* not executable

**Connect:** ```ssh bandit5@bandit.labs.overthewire.org -p 2220```


<br />
<br />

## Level 20-21
**Task:** The password for the next level is stored somewhere on the server and has all of the following properties:

* owned by user bandit7
* owned by group bandit6
* 33 bytes in size

**Connect:** ```ssh bandit6@bandit.labs.overthewire.org -p 2220```





We will continue level 31 in the next part.


