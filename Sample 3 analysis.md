
# Static Analysis

MD5 hash: 75D395F3B1458696FE3421CF1938F153
SHA1 hash: BB99977D354623FA0968AA579E1C4298B2A304AD

![[Pasted image 20260502095222.png]]

Suspicious company name and product name 

# Dynamic Analysis

The process is run in the background without any visible windows.

![[Pasted image 20260502100227.png]]

The sample creates a `cmd.html` file. Initially the contents of the file is empty

![[Pasted image 20260502095817.png]]

After looking at the `cmd.html` file it is clear that the sample is a keylogger 

![[Pasted image 20260502100342.png]]

# Network activity

The sample does not make any outgoing requests, this might indicate that it only communicates after a certain period of time.

