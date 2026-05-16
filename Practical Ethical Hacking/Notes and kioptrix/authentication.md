using burpsuite:

send to intruder, mark password
load a wordlist in the payload

Fffuf:

copy the request from burp and add FUZZ to the password
```
ffuf -request req.txt -request-proto http  -w /usr/share/wordlists/share/seclists/Passwords/xato.... -fs (filter size)
```

# MFA

some sites use the same code for authentication, so we can login as a different user and edit the user in the post request to login 

you can also try to bruteforce the code if its weak enough 



# limited login attemps

use n-1 attempts to bruteforce using clusterbomb and use the top n passwords for the list

```
users.txt
admin
jessamy
jeremy 
info


pass.txt

password
Password123
letmein
123456

```

clusterbomb in burpsuite

