
### command line 

`<user name>@<host name>: <pwd> $ `

```
whoami 
hostname 
pwd
ls
cd
```

getting help:
```
man 
info (more detailed and documented)
--help
```

https://explainshell.com

if all fails, google 


### more or less

more - displays one page at a time, no going back

less - pretty similar, multi directional 
can be used to search using / , next occurence using n

less offers more functionality 

cat - concatenate or list contents of a file.

-n numbers all lines 
-b numbers non empty lines


## head and tail
print first or last 10 lines 

diff - show differencees between two files.

[[Files and filesystem]]

## Linking files

basically like shortcuts in windows 
can be created using the `ln` command 
-S - soft link

two types of links:
hard links and soft links

hard links - point to the actual data in memory, removing the original will still keep the link with contents 

soft links - points to a existing file , if original file is deleted the link is broken.
