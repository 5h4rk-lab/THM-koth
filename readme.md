# food-Koth.
First,do a basic nmap scan and then you would find some deatiles about the IP address.<br/>
from that you can get the first flag and a user by the ssh credentials with the help of mysql database.<br/>
after getting the shell now its time to get the root.<br/>
so use find command and search for the vulnerbility.<br/>
find / -perm -u=s -type f 2>/dev/null<br/>


from this scan you will find out the available options i found that "/usr/bin/vim.basic"<br/>
is available.so,what are you waiting for just get the password changed by<br/>
vim /etc/passwd<br/>
and change the passwd thats it then just login with root and your password.<br/>
