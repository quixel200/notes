
# Static Analysis

MD5 hash: 57ACEF15E788C73FCBBFD66B0C8A6FE2
SHA1 Hash: 07E1B0B8AEDC88DB7A5E1AB451091BBB31962AA7

The internal name of the file is "KHATRA". 

# Dynamic Analysis

Once renaming the folder to an exe, it immediately changes to a folder icon while hiding the exe extension.
![[Pasted image 20260429160309.png]]


The sample file immediately drops 3 exes upon running, namely:
- KHATRA.exe
- Xplorer.exe
- gHost.exe

It also runs a hidden command prompt window

![[Pasted image 20260429160755.png]]

We can view the properties and see what the command being run is
![[Pasted image 20260429160858.png]]

```
C:\WINDOWS\system32\cmd.exe /C netsh firewall add allowedprogram program=C:\WINDOWS\system32\KHATRA.exe name=System
```
This allows the program to communicate freely without being restricted by the windows firewall


Suspicious new registry keys have been added 
![[Pasted image 20260430083732.png]]


After running the sample, procmon and process explorer immediately crash on startup. This indicates virus like behavior 


