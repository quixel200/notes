reverse shell - 
attacker is listening, victim connects
bind shell - 
victim is listening, attacker connects

### staged vs non-staged payloads

Non- staged:
sends exploit shellcode all at once
larger in size
doesnt always work
example:
**windows/meterpreter_reverse_tcp**

Staged:
sends payload in stages
can be less stable
example:
**windows/meterpreter/reverse_tcp**

# Brute forcing 
Use hydra or metasploit auxilarry modules.
/usr/share/wordlists 

# Credential stuffing
injecting breached account credentials in hopes of accont takeover.

Use Intruder in burpsuite to perform the attack.



# gaining root

![[Pasted image 20240720133612.png]]

successfuly gained access to the system using smb exploit trans2open using metasploit.

manual exploitation:

![[Pasted image 20240720134435.png]]

gained initial access with exploiting modssl 

