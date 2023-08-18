---
tags: cisco
---

 Redundancy in networks

it is essential part of network 

#### it is a layer 2 protocol

![[Pasted image 20230708000359.png]]

when pc1 wants to find the pc2's ip address it sends a broadcast request to the switch and forwards the request to all the domains 

if so the pc2 is found on the network and responded to pc1 the broadcast frames remains in the network and it caused broadcast storm which causes the network to look like this
![[Pasted image 20230708000617.png]]


![[Pasted image 20230708001055.png]]

Spanning tree protocol was developed for bridge but in these days it it really means it is used ofr switch. bridges are not used in modern networks

![[Pasted image 20230708001342.png]]
here in the given diagram the green dot represents the ports are in forwarding state

what tstp does is it makes the connection like the below by making sw3 in blocking state  

![[Pasted image 20230708001328.png]]

if pc1 sends a broadcast frame no loops are created as we have disabled the path causing loop

#### what happens if the connection btw sw1 ans sw2 fails?
![[Pasted image 20230708001630.png]]
The protocol will automatically adjust 

![[Pasted image 20230708001712.png]]
![[Pasted image 20230708001935.png]]
![[Pasted image 20230708002001.png]]

![[Pasted image 20230708002317.png]]

![[Pasted image 20230708002456.png]]


![[Pasted image 20230708002928.png]]
### let us compare the cost for the following
![[Pasted image 20230708003135.png]]
since switch 1 has least mac address it is chosen as the root bridge

> the cost of reaching the root from sw1 is 0
> the cost of reaching the root from sw2 is from port 60/1 becomes 4 and g0/0 becomes 8
> the cost of reaching the root from sw3 is from port g0/1 becomes 8 and g0/0 becomes 4

![[Pasted image 20230708003432.png]]

 ![[Pasted image 20230708004212.png]]



### Some of the spanning tree concepts

STP states/timers,bpdu,optional features,configuration


There are 4+1 types of states

#### Blocking
non-designated ports remains stable in a blocking state
interface in blocking states are disabled to prevent loops
interface in blocking states do not send or recieve network traffic
interface in a blocking state do not revieve or send bpdus
and they do'nt learn mac address

### Forwarding state
Root /Designated ports remains in forwarding state

### Listening state
>after blocking state.interfaces with the designated or root role enters Listening state.

>only designated or root ports enters listening states

>it is 15 seconds long by default

>An interface in the listening state only forwards stp BPDUS

>it does not send/receive regular traffic

>an interface in the listening state does not learn mac addresses from regular traffic that arrives on the interface

![[Pasted image 20230709055033.png]]
![[Pasted image 20230709055416.png]]

![[Pasted image 20230709060805.png]]

the spanning tree pdu contains root identifier which contains the details of the root node
_Bridge identifier_  contains the details of the bridge 
hello,fwd delay and max age are also present


### Spanning tree optional features (STP Toolkit)

### Portfast
It allows a port to move immediately to the forwarding state, bypassing Listening and Learning
If it is used it must be only enabled on ports connected to end hosts
if enabled on port connected to another switch it may cause layer 2 loop
```bash
Switch#sh ip int brief

Interface IP-Address OK? Method Status Protocol

FastEthernet0/1 unassigned YES manual up up

FastEthernet0/2 unassigned YES manual up up

FastEthernet0/3 unassigned YES manual up up

FastEthernet0/4 unassigned YES manual down down

FastEthernet0/5 unassigned YES manual down down

FastEthernet0/6 unassigned YES manual down down

FastEthernet0/7 unassigned YES manual down down

FastEthernet0/8 unassigned YES manual down down

FastEthernet0/9 unassigned YES manual down down

FastEthernet0/10 unassigned YES manual down down

FastEthernet0/11 unassigned YES manual down down

FastEthernet0/12 unassigned YES manual down down

FastEthernet0/13 unassigned YES manual down down

FastEthernet0/14 unassigned YES manual down down

FastEthernet0/15 unassigned YES manual down down

FastEthernet0/16 unassigned YES manual down down

FastEthernet0/17 unassigned YES manual down down

FastEthernet0/18 unassigned YES manual down down

FastEthernet0/19 unassigned YES manual down down

FastEthernet0/20 unassigned YES manual down down

FastEthernet0/21 unassigned YES manual down down

FastEthernet0/22 unassigned YES manual down down

FastEthernet0/23 unassigned YES manual down down

FastEthernet0/24 unassigned YES manual down down

GigabitEthernet0/1 unassigned YES manual down down

GigabitEthernet0/2 unassigned YES manual down down

Vlan1 unassigned YES manual administratively down down

Switch#

Switch#

Switch#conf t

Enter configuration commands, one per line. End with CNTL/Z.

Switch(config)#int F0/1

Switch(config-if)#sp

Switch(config-if)#spa

Switch(config-if)#spanning-tree portfast

%Warning: portfast should only be enabled on ports connected to a single

host. Connecting hubs, concentrators, switches, bridges, etc... to this

interface when portfast is enabled, can cause temporary bridging loops.

Use with CAUTION

  

%Portfast has been configured on FastEthernet0/1 but will only

have effect when the interface is in a non-trunking mode.

Switch(config-if)#

Switch(config-if)#end

Switch#

%SYS-5-CONFIG_I: Configured from console by console

  

Switch#write

Building configuration...

[OK]

Switch#

```

### BPDU GUARD
if bpdu from another interface is recieved the interface will shut down


![[Pasted image 20230709063016.png]]


![[Pasted image 20230709064528.png]]

in case the root bridge fails we can give secondary bridge as fallback using the following command 
![[Pasted image 20230709064850.png]]

### Mcqs
![[Pasted image 20230709065042.png]]
![[Pasted image 20230709065216.png]]

![[Pasted image 20230709065232.png]]



# Rapid STP

![[Pasted image 20230709065557.png]]

![[Pasted image 20230709065726.png]]

![[Pasted image 20230709065756.png]] 

![[Pasted image 20230709070120.png]]

![[Pasted image 20230709070403.png]]

![[Pasted image 20230709070310.png]]

![[Pasted image 20230709070510.png]]

### Backbone fast

![[Pasted image 20230709071708.png]]

If bpdu messages are not recieved from the switch 1 switch 2 assumes itself as the root bridge and starts to send its own bpdus 

switch 3 will ignore all of the sw2's bpdus until its non designated port turns to designated port

![[Pasted image 20230709071943.png]]

### Backup port

![[Pasted image 20230709072047.png]]

![[Pasted image 20230709072206.png]]

All switches running rstp sends their own BPDUs every hello time

in stf STP the switch waits 10 hello intervals , but in RSTP the switch flushes all the mac address and considers the neighbour is lost after 3 hello intervals

![[Pasted image 20230709073031.png]]

edge ports are like std spanning tree portfast since it is only 
![[Pasted image 20230709073155.png]]

![[Pasted image 20230709073447.png]]

![[Pasted image 20230709073535.png]]