# machine name for KOTH: food(linux)
First,do a basic nmap scan and then you would find details about the IP address.<br/>
from the scan we got to know that there is a sql database running on.<br/>
with the help of command
"mysql -u root -h <ip> -p"  login to sql database with pass root <br/>
with the help of mysql database explore the tables.that will get the first flag and a user by the ssh credentials <br/>
after getting the shell now its time to get the root.<br/>
so use find command and search for the vulnerbility.<br/>
find / -perm -u=s -type f 2>/dev/null<br/>
from this scan you will find out the available options i found that "/usr/bin/vim.basic"<br/>
is available.so,what are you waiting for just get the password changed by<br/>
vim /etc/passwd<br/> //dont forget to encrypt your password while changing!
and change the passwd thats it then just login with root and your password.<br/>
<hr>
