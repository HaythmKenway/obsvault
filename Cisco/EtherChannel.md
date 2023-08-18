---
tags: cisco
---


![[Pasted image 20230709084326.png]]

we have 2 switches access layer switch and distribution layer switch , the access layer switch has 40 nodes connected which is in turn connected to distribution layer switch

so we configure an etherchannel group so that multiple interfaces can act as single interface
this makes stp assume multiple interface as a single interface

![[Pasted image 20230709085651.png]]


![[Pasted image 20230709085320.png]]

since spanning tree protocol only allows a single connection between two nodes , only a single connection can be accessed by the distribution layer switch from the access layer switch

### Loadbalancing

![[Pasted image 20230709090049.png]]

 


a single connection cannot handle all the requests from the node so multiple connections are made between the two devices

# methods of configuring etherchannel

![[Pasted image 20230709075527.png]]

UPTO 8 interfaces can be formed into a single ether channel 
lacp allows 16, but only 8 will be active and rest are standby

![[Pasted image 20230709092047.png]]

Configurations to create ether channel
![[Pasted image 20230709092147.png]]
![[Pasted image 20230709092200.png]]

# on only works with on

