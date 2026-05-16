
Dividing a network into smaller sub networks is called subnetting. It allows for more efficient use of IP addresses(network management and routing).

CIDR (Classless Inter-Domain Routing) notation is a method used to represent IP addresses and their corresponding subnet masks

A common subet we see is /24 which is used by our home networks.
allows for 256 hosts (technically 254 cuz we need one for network id and one for broadcast)
the subnet mask for this range would be 255.255.255.0.

![[Pasted image 20240713105201.png]]

/24 indicates the the first 25 bits are used to represent the network portion of the IP address and the remaining 8 bits represent the host portion.

Network address - generally the first ip in the range
broadcast address - generally the last ip in the range

![[Pasted image 20240713105557.png]]

Examples:

![[Pasted image 20240713110730.png]]


calculator:
https://www.ipaddressguide.com/cidr
seven second subnetting:
https://www.youtube.com/watch?v=ZxAwQB8TZsM

