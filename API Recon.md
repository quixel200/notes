
Findings API:
request headers
response 
content type of XML/JSON 
api.website.com/v1....
website.com/api/v1....



## Passive recon

public information 

google, for eg, "reddit api"

![[Pasted image 20260404174853.png]]


## gitdorking

Begin by searching GitHub for your target organization’s name paired with potentially sensitive types of information, such as “api key,” "api keys", "apikey", "authorization: Bearer", "access_token", "secret", or “token.”

## Trufflehog

ruffleHog is a great tool for automatically discovering exposed secrets. You can simply use the following Docker run to initiate a TruffleHog scan of your target's Github.

 $ sudo docker run -it -v "$PWD:/pwd" trufflesecurity/trufflehog:latest github --org=target-name
## Shodan 

![[Pasted image 20260404174946.png]]

The waybackmachine (for zombie apis)


# Active Recon

```
nmap -sV --script=http-enum <target> -p 80,443,8000,8080
```

**OWASP Amass**

OWASP Amass is a command-line tool that can map a target’s external network by collecting OSINT from over 55 different sources. You can set it to perform passive or active scans

**`amass enum -active -d target-name.com |grep api`**

## gobuster

```
gobuster dir -u target-name.com:8000 -w /home/hapihacker/api/wordlists/common_apis_160
```

## Kiterunner

```
kr scan HTTP://127.0.0.1 -w ~/api/wordlists/data/kiterunner/routes-large.kite
```


