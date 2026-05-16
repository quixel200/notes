
## sockets 

used to connect nodes together.
connecting to ports and ip addresses

```
import socket 

HOST = '127.0.0.1'
PORT = 1234

s = socket.socket(socket.AF_INET,socket.SOCK_STREAM) #af_inet is ipv4 and sock_stream is a port
s.connect((HOST,PORT))

```

a really bad implementation of a port scanner

```
#!/usr/bin/env python3

import sys,socket
from datetime import datetime

if len(sys.argv)==2:
    target = socket.gethostbyname(sys.argv[1])


else:
    print("usage: scanner.py <ip address>")

print("-"*50)
print("scanning target: ",target)
print("Time started: ",str(datetime.now()))
print("-"*50)

try:
    print("open ports:")
    for port in range(50,85):
        s = socket.socket(socket.AF_INET,socket.SOCK_STREAM)
        socket.setdefaulttimeout(1)
        result = s.connect_ex((target,port))
        if(result==0): 
            print("port {}".format(port))
        s.close()

except KeyboardInterrupt:
    print("\ninterrupt detected, exiting program")
    sys.exit()

except socket.giaerror:
    print("Hostname could not be resolved")
    sys.exit()

except socket.error:
    print("could not connect to server")
    sys.exit()
```