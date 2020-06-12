# machine name for KOTH: food(linux)
First,do a basic nmap scan and then you would find details about the IP address.<br/>
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
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service : <br/>
SF-Port9999-TCP:V=7.80%I=7%D=6/11%Time=5EE1FE52%P=x86_64-pc-linux-gnu%r(Ge <br/>
SF:tRequest,78,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Thu,\x2011\x20Jun\x2020 <br/>
SF:20\x2009:50:11\x20GMT\r\nContent-Length:\x204\r\nContent-Type:\x20text/ <br/> 
SF:plain;\x20charset=utf-8\r\n\r\nking")%r(HTTPOptions,78,"HTTP/1\.0\x2020 <br/>
SF:0\x20OK\r\nDate:\x20Thu,\x2011\x20Jun\x202020\x2009:50:11\x20GMT\r\nCon <br/>
SF:tent-Length:\x204\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\n\ <br/>
SF:r\nking")%r(FourOhFourRequest,78,"HTTP/1\.0\x20200\x20OK\r\nDate:\x20Th <br/>
SF:u,\x2011\x20Jun\x202020\x2009:50:12\x20GMT\r\nContent-Length:\x204\r\nC <br/>
SF:ontent-Type:\x20text/plain;\x20charset=utf-8\r\n\r\nking")%r(GenericLin <br/>
SF:es,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plai <br/>
SF:n;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Reques <br/>
SF:t")%r(RTSPRequest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Typ <br/>
SF:e:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x <br/>
SF:20Bad\x20Request")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCon <br/>
SF:tent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\ <br/>
SF:r\n400\x20Bad\x20Request")%r(SSLSessionReq,67,"HTTP/1\.1\x20400\x20Bad\ <br/>
SF:x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnecti <br/>
SF:on:\x20close\r\n\r\n400\x20Bad\x20Request")%r(TerminalServerCookie,67," <br/>
SF:HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20c <br/>
SF:harset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(T <br/>
SF:LSSessionReq,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x2 <br/>
SF:0text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad <br/>
SF:\x20Request")%r(Kerberos,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCont <br/>
SF:ent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r <br/>
SF:\n400\x20Bad\x20Request")%r(LPDString,67,"HTTP/1\.1\x20400\x20Bad\x20Re <br/>
SF:quest\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x <br/>
SF:20close\r\n\r\n400\x20Bad\x20Request")%r(LDAPSearchReq,67,"HTTP/1\.1\x2 <br/>
SF:0400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf-8 <br/>
SF:\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(SIPOptions,67 <br/>
SF:,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x2 <br/>
SF:0charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request"); <br/>

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ . <br/>
<hr>
<hr>


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

 #### Nmap 7.80 scan initiated Thu Jun 11 14:19:26 2020 as: nmap -sC -sV -oN nmap.txt 10.10.173.121 <br/>
 <p>
Nmap scan report for 10.10.173.121<br/>
Host is up (0.16s latency).<br/>
Not shown: 991 closed ports<br/>
PORT     STATE    SERVICE     VERSION <br/>
22/tcp   open     ssh         OpenSSH 7.4 (protocol 2.0)<br/>
| ssh-hostkey: <br/>
|   2048 46:6c:5a:31:5f:c1:1f:f3:65:e7:64:f2:c5:f5:59:d8 (RSA)<br/>
|   256 5d:a5:8a:af:1e:21:48:7a:04:22:3e:4a:f5:e4:5b:02 (ECDSA)<br/>
|_  256 6a:44:1c:e1:15:c9:5e:94:da:06:8d:db:d2:bc:66:54 (ED25519)<br/>
80/tcp   open     http        Apache httpd 2.4.6 ((CentOS) PHP/7.3.16)<br/>
| http-methods: <br/>
|_  Potentially risky methods: TRACE <br/>
|_http-server-header: Apache/2.4.6 (CentOS) PHP/7.3.16 <br/>
|_http-title: Site doesn't have a title (text/html; charset=UTF-8). <br/>
139/tcp  open     netbios-ssn Samba smbd 3.X - 4.X (workgroup: SAMBA) <br/>
445/tcp  open     netbios-ssn Samba smbd 4.9.1 (workgroup: SAMBA) <br/>
3306/tcp open     mysql       MariaDB (unauthorized) <br/>
5000/tcp open     http        Werkzeug httpd 1.0.0 (Python 3.6.8) <br/>
|_http-server-header: Werkzeug/1.0.0 Python/3.6.8 <br/>
|_http-title: Tyler's file upload <br/>
8080/tcp open     http        nginx 1.16.1 <br/>
| http-robots.txt: 1 disallowed entry <br/>
|_/ <br/>
|_http-server-header: nginx/1.16.1 <br/>
| http-title: LibreNMS <br/>
|_Requested resource was http://10.10.173.121:8080/login <br/>
|_http-trane-info: Problem with XML parsing of /evox/about <br/>
8088/tcp filtered radan-http <br/>
9999/tcp open     abyss? <br/>
| fingerprint-strings: <br/>
|   FourOhFourRequest, HTTPOptions: <br/> 
|     HTTP/1.0 200 OK <br/>
|     Accept-Ranges: bytes <br/>
|     Content-Length: 1 <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|     Last-Modified: Thu, 26 Mar 2020 11:36:37 GMT <br/>
|     Date: Thu, 11 Jun 2020 08:50:10 GMT <br/>
|   GenericLines, Help, Kerberos, LPDString, RTSPRequest, SSLSessionReq, TLSSessionReq, TerminalServerCookie: <br/> 
|     HTTP/1.1 400 Bad Request <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|     Connection: close <br/>
|     Request <br/>
|   GetRequest: <br/>
|     HTTP/1.0 200 OK <br/>
|     Accept-Ranges: bytes <br/>
|     Content-Length: 1 <br/>
|     Content-Type: text/plain; charset=utf-8 <br/>
|     Last-Modified: Thu, 26 Mar 2020 11:36:37 GMT <br/>
|_    Date: Thu, 11 Jun 2020 08:50:09 GMT <br/>
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service : <br/>
SF-Port9999-TCP:V=7.80%I=7%D=6/11%Time=5EE1F040%P=x86_64-pc-linux-gnu%r(Ge <br/>
SF:tRequest,B9,"HTTP/1\.0\x20200\x20OK\r\nAccept-Ranges:\x20bytes\r\nConte <br/>
SF:nt-Length:\x201\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nLas <br/>
SF:t-Modified:\x20Thu,\x2026\x20Mar\x202020\x2011:36:37\x20GMT\r\nDate:\x2 <br/>
SF:0Thu,\x2011\x20Jun\x202020\x2008:50:09\x20GMT\r\n\r\n\n")%r(HTTPOptions <br/>
SF:,B9,"HTTP/1\.0\x20200\x20OK\r\nAccept-Ranges:\x20bytes\r\nContent-Lengt <br/> 
SF:h:\x201\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nLast-Modifi <br/>
SF:ed:\x20Thu,\x2026\x20Mar\x202020\x2011:36:37\x20GMT\r\nDate:\x20Thu,\x2 <br/>
SF:011\x20Jun\x202020\x2008:50:10\x20GMT\r\n\r\n\n")%r(FourOhFourRequest,B <br/>
SF:9,"HTTP/1\.0\x20200\x20OK\r\nAccept-Ranges:\x20bytes\r\nContent-Length: <br/>
SF:\x201\r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nLast-Modified <br/>
SF::\x20Thu,\x2026\x20Mar\x202020\x2011:36:37\x20GMT\r\nDate:\x20Thu,\x201 <br/>
SF:1\x20Jun\x202020\x2008:50:10\x20GMT\r\n\r\n\n")%r(GenericLines,67,"HTTP <br/>
SF:/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20chars <br/>
SF:et=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(RTSPR <br/>
SF:equest,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/ <br/>
SF:plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Re <br/>
SF:quest")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\ <br/>
SF:x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20B <br/>
SF:ad\x20Request")%r(SSLSessionReq,67,"HTTP/1\.1\x20400\x20Bad\x20Request\ <br/>
SF:r\nContent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20clos <br/>
SF:e\r\n\r\n400\x20Bad\x20Request")%r(TerminalServerCookie,67,"HTTP/1\.1\x <br/>
SF:20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain;\x20charset=utf- <br/>
SF:8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request")%r(TLSSessionRe <br/> 
SF:q,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20text/plain <br/>
SF:;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x20Request <br/>
SF:")%r(Kerberos,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x <br/>
SF:20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Ba <br/>
SF:d\x20Request")%r(LPDString,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nCo <br/>
SF:ntent-Type:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n <br/>
SF:\r\n400\x20Bad\x20Request"); <br/>
Service Info: Host: TYLER <br/>

Host script results: <br/>
|_clock-skew: mean: 1h20m01s, deviation: 2h18m34s, median: 0s <br/>
|_nbstat: NetBIOS name: TYLER, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown) <br/>
| smb-os-discovery: <br/>
|   OS: Windows 6.1 (Samba 4.9.1) <br/>
|   Computer name: tyler <br/>
|   NetBIOS computer name: TYLER\x00 <br/>
|   Domain name: \x00 <br/>
|   FQDN: tyler <br/>
|_  System time: 2020-06-11T04:51:37-04:00 <br/>
| smb-security-mode: <br/>
|   account_used: guest <br/>
|   authentication_level: user <br/>
|   challenge_response: supported <br/>
|_  message_signing: disabled (dangerous, but default) <br/>
| smb2-security-mode: <br/>
|   2.02: <br/>
|_    Message signing enabled but not required <br/>
| smb2-time: <br/>
|   date: 2020-06-11T08:51:38 <br/>
|_  start_date: N/A <br/>

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ . <br/>

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



