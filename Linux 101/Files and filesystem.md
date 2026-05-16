
`man hier`
really cool

/bin - stores executable programs 
/boot - well...its boot
/dev - they're all devices wtf
/etc - configuration files for the system
/home - contains the personal directories for users
/lib - needed for programs for run
/media - mount point for removable devices
/mnt - also mount point for temporary mounted filesystems
/opt - software that isnt installed by the package manager
/proc - information on running proccesses.
/root - home directory of root user
/sbin - commands usually executed by superuser
/tmp - temporary files
/usr - contains ./bin, important commands 
	./local - programs installed specifically for the system
/var - 
	./log - contains log files(syslog)

## Partitions

/etc/fstab - contains filesystem info

mount - mount or view mounted devices
df - disk file space usage (-h more readable)
du - disk usage of files and directories on the system.

## Path expansion or Globbing:

```
* - Matches any character
? - matches one character
** - matches 0 or more characters accross directories(shopt -s globstar)
[] - match specific characters
```
