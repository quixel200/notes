-oHostKeyAlgorithms=+ssh-rsa
for ssh login

We got access to the machine, so we have done:
information gathering
scanning and enumeration
exploitation

now we repeat the process

## system enumeration

gives kernal info
```
uname -a 
cat /proc/version
cat /etc/issue
lscpu (cpu info)
```
service info
```
ps aux
ps aux | grep root
```

## user enumeration

```
whoami
id
sudo -l
cat /etc/passwd
history
```

look for access to sensitive files like /etc/shadow
/etc/group

## network enumeration

```
ifconfig or
ip a
```
sometimes a machine can run on two networks
```
ip route
```
arp tables - tells us who we are communicating with
```
arp -a or
ip neigh
netstat -ano
```
identify open ports and communications 


## password hunting 

```
grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null

find / -name id_rsa 2> /dev/null
```

## automated tools

LinPeas - [https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS](https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite/tree/master/linPEAS)

LinEnum - [https://github.com/rebootuser/LinEnum](https://github.com/rebootuser/LinEnum)

Linux Exploit Suggester - [https://github.com/mzet-/linux-exploit-suggester](https://github.com/mzet-/linux-exploit-suggester)

Linux Priv Checker - [https://github.com/sleventyeleven/linuxprivchecker](https://github.com/sleventyeleven/linuxprivchecker)

