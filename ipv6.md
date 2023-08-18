                 
---
tags: cisco
---
![[Pasted image 20230710201046.png]]

shortening ipv6

![[Pasted image 20230710201420.png]]

FE80::2:0:0:FBE8
AE89:2100:01ac:00F0::020F
2001:DB8:8b00:1000:2:BC0:D07:99
2001:DB8::1000


Typically an enterprise requesting ipv6 addressing from their isp will recieve a 48 bit block

they use a /64 prefix length
so the enterprise has 16 bits to use to make subnets
the remaining 64 bits can be used for hosts


Ipv6 address types:-

Global unicast
unique local
link local
multicast
others

  

# finding EUI 64 bit id

take mac address (48 bits)
break it into two halves
invert the 7th bit 


![[Pasted image 20230711021515.png]]


![[Pasted image 20230711021642.png]]
 

![[Pasted image 20230711021727.png]]
![[Pasted image 20230711021750.png]]

![[Pasted image 20230711022055.png]]

![[Pasted image 20230711022212.png]]
![[Pasted image 20230711022824.png]]



### ipv6 header
![[Pasted image 20230711023516.png]]


Solicitated node multicast address

![[Pasted image 20230711023632.png]]

### NDP

neighbour discovery protocol is created to replace arp in ipv6

![[Pasted image 20230711024748.png]]


![[Pasted image 20230711025116.png]]


![[Pasted image 20230711025612.png]]

![[Pasted image 20230711025652.png]]
![[Pasted image 20230711025813.png]]

