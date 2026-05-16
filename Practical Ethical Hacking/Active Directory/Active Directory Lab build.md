
windows 10 enterprise edition 
windows server 2022

Click on windows server 2022(desktop experience) when installing 

once the windows server opens 
Manage -> add roles and features -> role based/feature installation
set up the domain controller 

Ive used nier theme.
so its YoRha 

and its hostname is nier.local

next login to that account,
set up a certificate service thing.

Set up 2 user machines 
thePunisher 
the Bunker 

usernames:
9S
2B
password:
Password1

change the pc name:
THEPUNISHER
THEBUNKER

Next boot up the domain controller
tools -> active directory users and computers

right click on nier.local
new -> OU
call it groups
move all the random user groups there
just need admin and guest.

make another admin
right click on admin->copy

pascal
password123!

copy admin again 
create a service account 
SQLService
MYpassword123#

![[Pasted image 20240725100505.png]]
very common


create user accounts

right click -> new user
2B
Password1


A2
Password2

create file share

file and storage services -> shares -> new share
called backdoor

open cmd as admin
```
setspn -a YoRha-DC/SQLService.nier.local:60111 nier\SQLService

spn -T nier.local -Q */* to query
we should see existing spn found
```

open group policy management 

right click on nier.local, create a new GPO in this domain...
call it 'Disable Windows Defender'

right click-> edit

computer configuration -> policies -> administrative templates -> windows components -> microsoft defender antivirus

turn off windows defender -> enabled.

right click on the policy.
enforced

![[Pasted image 20240725102335.png]]


Configure user machines

change ipv4 properties
use dns:
set to ip of DC

on the punisher:
edit local user and groups

enable admin account by setting password
Password1!

add pascal to the admin group
pascal = fcastle in the vid
no its actually 2b i think

do the same for the bunker 
make sure the password for admin is same

add a2 and pascal in admin group

![[Pasted image 20240725172825.png]]
connect using different credentials

# ip addresses

DC - 10.0.2.15

ThePunisher - 10.0.2.10
theBunker - 10.0.2.9