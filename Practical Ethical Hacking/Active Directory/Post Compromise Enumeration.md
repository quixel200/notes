## domain enumeration - ldapdomaindump

```
sudo ldapdomaindump ldaps://10.0.2.15 -u 'NIER\2B' -p Password1
```

![[Pasted image 20240728182837.png]]
## bloodhound 

credentials:
neo4j
neo4j (this is default, will change)
```
sudo neo4j console
sudo bloodhound
```

use the neo4j credentials to log in to bloodhound
```
mkdir bloodhound
cd 

sudo bloodhound-python -d nier.local -u 2B -p Password1 -ns 10.0.2.15 -c all
(injester that collects data)
```
in bloodhound:
upload data
select all the jsons in the dir

## plumhound 

install through github repo(use pip3)

make sure bloodhound is open
```
sudo python3 PlumHound.py --easy -p <neo4j password>
```
this is just a quick query of the domain

```
sudo python3 PlumHound.py -x tasks/default.tasks -p neo4j1
```
will put all the stuff in reports folder
look at index.html
![[Pasted image 20240728184159.png]]


## pingcastle

has a free download for personal use and auding your own systems.
\
# [[Post Compromise attacks]]
