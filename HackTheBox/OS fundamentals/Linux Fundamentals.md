Philosophy:

- `Everything is a file`
- `Small, single-purpose programs`
- `Ability to chain programs together to perform complex tasks`
- `Avoid captive user interfaces`
- `Configuration data stored in a text file`

| Component         | Description                                                                                                                                                                                                                                                                                                                                     |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Bootloader`      | A piece of code that runs to guide the booting process to start the operating system. Parrot Linux uses the GRUB Bootloader.                                                                                                                                                                                                                    |
| `OS Kernel`       | The kernel is the main component of an operating system. It manages the resources for system's I/O devices at the hardware level.                                                                                                                                                                                                               |
| `Daemons`         | Background services are called "daemons" in Linux. Their purpose is to ensure that key functions such as scheduling, printing, and multimedia are working correctly. These small programs load after we booted or log into the computer.                                                                                                        |
| `OS Shell`        | The operating system shell or the command language interpreter (also known as the command line) is the interface between the OS and the user. This interface allows the user to tell the OS what to do. The most commonly used shells are Bash, Tcsh/Csh, Ksh, Zsh, and Fish.                                                                   |
| `Graphics server` | This provides a graphical sub-system (server) called "X" or "X-server" that allows graphical programs to run locally or remotely on the X-windowing system.                                                                                                                                                                                     |
| `Window Manager`  | Also known as a graphical user interface (GUI). There are many options, including GNOME, KDE, MATE, Unity, and Cinnamon. A desktop environment usually has several applications, including file and web browsers. These allow the user to access and manage the essential and frequently accessed features and services of an operating system. |
| `Utilities`       | Applications or utilities are programs that perform particular functions for the user or another program.                                                                                                                                                                                                                                       |

## Architecture 
The Linux operating system can be broken down into layers:

|**Layer**|**Description**|
|---|---|
|`Hardware`|Peripheral devices such as the system's RAM, hard drive, CPU, and others.|
|`Kernel`|The core of the Linux operating system whose function is to virtualize and control common computer hardware resources like CPU, allocated memory, accessed data, and others. The kernel gives each process its own virtual resources and prevents/mitigates conflicts between different processes.|
|`Shell`|A command-line interface (**CLI**), also known as a shell that a user can enter commands into to execute the kernel's functions.|
|`System Utility`|Makes available to the user all of the operating system's functionality.|
## file system hierarchy
[[Files and filesystem]]


# Distros

debian - stable and reliable 
uses apt (advanced package manager)

# shell 
prompt description:
```shell-session
<username>@<hostname><current working directory>$
```

# for help

use man 
or --help

# sysinfo

uname,id,whoami,who etc.

-i = find the index number of file

ls -lt = last modified

# finding files and directories

which
find
`-exec ls -al {} \;`

locate


# file descriptors and redirections

stdin = 0
stdout = 1
stderr = 2

pipes, input/output redirection etc.

# regex

![[Pasted image 20240826124001.png]]

-E - extended regex

