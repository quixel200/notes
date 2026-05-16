
machine ip: 10.0.2.152

# nmap scan

![[Pasted image 20240720182956.png]]

FTP open with anonymous logins.
ssh - meh,whatever

http on port 80 with default page
apache 2.4.38

![[Pasted image 20240720185242.png]] 
information disclosure



ftp contains sensitive files. Information disclosure

```
Hello Heath !
Grimmie has setup the test website for the new academy.
I told him not to use the same password everywhere, he will change it ASAP.


I couldn't create a user via the admin panel, so instead I inserted directly into the database with the following command:

INSERT INTO `students` (`StudentRegno`, `studentPhoto`, `password`, `studentName`, `pincode`, `session`, `department`, `semester`, `cgpa`, `creationdate`, `updationDate`) VALUES
('10201321', '', 'cd73502828457d15655bbd7a63fb0bc8', 'Rum Ham', '777777', '', '', '', '7.60', '2021-05-29 14:36:56', '');

The StudentRegno number is what you use for login.


Le me know what you think of this open-source project, it's from 2020 so it should be secure... right ?
We can always adapt it to our needs.

-jdelta

```
10201321:cd73502828457d15655bbd7a63fb0bc8

# hash-identifier - built into kali


Directory bruteforce found something.

![[Pasted image 20240720190044.png]]


![[Pasted image 20240720190005.png]]
phpmyadmin 4.9.7

# ffuz 

```
ffuf -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt:FUZZ -u http://10.0.2.7/FUZZ

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://10.0.2.7/FUZZ
 :: Wordlist         : FUZZ: /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

#                       [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 4ms]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/  [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 4ms]
# Attribution-Share Alike 3.0 License. To view a copy of this  [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 7ms]
                        [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 12ms]
# on atleast 2 different hosts [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 11ms]
# Priority ordered case sensative list, where entries were found  [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 14ms]
#                       [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 9ms]
# Copyright 2007 James Fisher [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 715ms]
#                       [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 719ms]
# This work is licensed under the Creative Commons  [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 772ms]
# directory-list-2.3-medium.txt [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 779ms]
#                       [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 1598ms]
# Suite 300, San Francisco, California, 94105, USA. [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 1608ms]
# or send a letter to Creative Commons, 171 Second Street,  [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 1624ms]
academy                 [Status: 301, Size: 306, Words: 20, Lines: 10, Duration: 5ms]
phpmyadmin              [Status: 301, Size: 309, Words: 20, Lines: 10, Duration: 5ms]
                        [Status: 200, Size: 10701, Words: 3427, Lines: 369, Duration: 24ms]
server-status           [Status: 403, Size: 273, Words: 20, Lines: 10, Duration: 22ms]

```
academy page.


weak credentials
![[Pasted image 20240720191413.png]]

image upload option allows for malicious docs, gained reverse shell.
![[Pasted image 20240721155756.png]]


```
/var/www/html/academy/admin/includes/config.php:$mysql_password = "My_V3ryS3cur3_P4ss";
/var/www/html/academy/includes/config.php:$mysql_password = "My_V3ryS3cur3_P4ss";

```
password reuse, can use ssh to login.

