
run pimpmykali in the vm


## Basic network commands 

```
ip a

ifconfig (older)
iwconfig 

ip r (show routing)

systemctl (can be used to start and stop services)

arp -a

netstat -rn (routing table)


```


## bash scripting 

ping sweeper:

```
#!/bin/bash

if [ "$1" == "" ]
then 
echo "you forgor"
echo "syntax: ./ping_sweep.sh x.x.x"

else
for ip in `seq 1 254`; do
        ping -c 1 $1.$ip | grep "64 bytes" | cut -d " " -f 4 | tr -d ":" &
done
fi

```

for nmap:

for ip in $(cat ips.txt);do nmap $ip; done
