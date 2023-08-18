---
tags: cisco
---
virtual lans

it is virtualizing local area network on local switches

### What is VLAN
virtual Lans 
Vlan is a single brodcast domain or logical network




![[Pasted image 20230703235759.png]]

![[Pasted image 20230704000446.png]]


### Paradigm of vlan

1) physical topology
2) Logical topology
![[Pasted image 20230704000539.png]]

![[Pasted image 20230704000547.png]]
logincal typologies are ed and green vlan

here a and d are connected in a network and c and b are connected inside a network 


### packet flow in same vlan
a packet from source address A can reach the Destination address D via the switch as they both are in the same vlan

#### Packet to other vlan
a packet from source address A cannot reach the Destination address C because it is in different subnet and hence requires a router to route packets between the subnets

### Broadcast packet flow

The frames are transmitted to all the nodes in the subnet

![[Pasted image 20230704001809.png]]


![[Pasted image 20230711202838.png]]



we have connected two switches via a trunk on 0/3

since the A and D belong to same vlan (red) packet can be transmitted

## Native Vlan

![[Pasted image 20230706083825.png]]

we have a configuration in which the switch is connected to an cisco ip phone and then we have configured pc to connect to ip phone which has its default switch and hen the switch is connected to the pc

Thie phone can be configured in seperate vlan so that pc cannot sniff the voice traffic

Voice franes can be tagged

### we can use VMPS to dynamically assign ip in the vlan


### VTP
it is a layer 2 cisco propriatory protocol, it allows propagation of vlan information
![[Pasted image 20230706085152.png]]


By default the nodes in the vtp are assignned to null domain 
the domains can be custmized with cisco commads.

it is layer 2 protocol

it  has a concept called revision no

when a change is made in a database the revision no is incremented and all the devices are updated to the latest revision

it contains the vlan database

### VTP MESSAGE
![[Pasted image 20230706085915.png]]

![[Pasted image 20230706090039.png]]
v![[Pasted image 20230706090053.png]]

### Drawbacks of VTP

![[Pasted image 20230706090234.png]]

introduction of a new switch with a higher revision number may cause the entire network to fail deleting the previous configuration

Hence vtp is not used by the network engineers

[[spanning tree protocol]]
