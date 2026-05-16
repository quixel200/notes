# Static Analysis

MD5 Hash: 41D5F78E918B22676AE1EE993C3C8C7F
SHA1 Hash: 0E72FA141E88F1A8C0EF0E51CE952B8C773B647D

The same is not verified and does not contain any metadata about the developer.
It also looks like a folder once renamed to a .exe file


# Dynamic Analysis 

The sample runs in a hidden window, and spawns a new exe process `yiatio.exe`

![[Pasted image 20260503130855.png]]

The dropped exe can be found in:
`C:\Documents and Settings\Siva\yiatio.exe`

Upon running the sample again, it drops a differently named exe, this means that the name of the exe is random upon each run.
![[Pasted image 20260503132253.png]]


The sample also communicates with an outside domain, and seems to initiate a connection on port 8000.

![[Pasted image 20260503131104.png]]


The sample also adds a Run registry key for persistence, and also changes the registry key to hide super hidden files.

![[Pasted image 20260503132202.png]]

Looking at the strings of the dropped exe, we see some personal information 

![[Pasted image 20260503132840.png]]

They also indicate that libraries for VBA have been imported, this might be a sign of infecting documents using macros. 

