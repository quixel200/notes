
# Static Analysis

MD5 Hash: 00A78B0E4BAC5345C7A59CAAA7A7ED4A
SHA1 Hash: E90A3EDCAE7EB83B7D97F4581F98170D0FE7FC9A

Architecture - x86, 32 bit binary


![[Pasted image 20260426114249.png]]

The description and author suggest that this is a trojan disguised as a compiler. The binary does not seem to be packed. 


# Dynamic Analysis 

Upon running the sample, it simply spawns a new dll process and then kills itself as seen in process explorer.

We can conclude that the original sample is just a dropper and the "tazebama.dll" seems to be the actual payload.

![[Pasted image 20260426115420.png]]

# Network Activity

Once the dll starts running, we can see outgoing network requests to `http[:]//www[.]britishcouncil[.]com` and another connection on port 80

![[Pasted image 20260426115327.png]]

We can see that it tries to open a connection from port 1062 to port 80, the purpose of this might be exfiltration.

![[Pasted image 20260426115358.png]]


# File system and registry changes 

The sample modifies the following registry keys to hide file extensions and hidden folders from being shown to the user. Toggling the option in file explorer will not affect it and the files will still be hidden. 

```
HKU\S-1-5-21-1202660629-926492609-839522115-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\HideFileExt: 0x00000000
HKU\S-1-5-21-1202660629-926492609-839522115-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\HideFileExt: 0x00000001
HKU\S-1-5-21-1202660629-926492609-839522115-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\ShowSuperHidden: 0x00000001
HKU\S-1-5-21-1202660629-926492609-839522115-1005\Software\Microsoft\Windows\CurrentVersion\Explorer\Advanced\ShowSuperHidden: 0x00000000
```

Looking at the file changes, we can see that the second stage was dropped in 
`C:\Documents and Settings\tazebama.dll`

We can also see another suspicious file:
`C:\Documents and Settings\Siva\Application Data\tazebama\zPharaoh.dat`

Opening this file, we can see that the sample seems to be collecting Emails and saving them to this file 

![[Pasted image 20260426120738.png]]

We can also see that the sample seems to modify all exe's that it can find, indicating virus like capabilities 

![[Pasted image 20260426120930.png]]

It also drops a "zPharaoh.exe" and a "autorun.inf" file in all the drives that it can find.
An `autorun.inf` file is a text file placed in the root directory of drives (USB, CD/DVD) to instruct Windows to automatically run an application, change icons, or define label names.

![[Pasted image 20260426121111.png]]

The sample also seems to log everything in a folder that it creates under
`C:\Documents and Settings\Siva\Application Data\tazebama`

![[Pasted image 20260426121250.png]]

We can conclude that this sample is a trojan virus that pretends to be a legitimate compiler application that steals email Ids and has persistence in the form of autorun and a always running dll file. 

# Indicators of compromise 

| IOC                                      | Type | Name          | Context     |
| ---------------------------------------- | ---- | ------------- | ----------- |
| E90A3EDCAE7EB83B7D97F4581F98170D0FE7FC9A | SHA1 | we.exe        | Sample      |
| 93C50D844B2FF0DA0D6FBE108D1D30A483C7A0CE | SHA1 | tazebalam.dl_ | Dropped DLL |
| A6F764B330C714E0F0D098BE407123D578C2A3D5 | SHA1 | Zpharaoh.exe  | Dropped EXE |
