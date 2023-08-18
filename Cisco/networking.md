---
tags: cisco
---
[[VLan]]
so we are about to configure the network 192.168.1.0 into 4 subnets
the req no of bits are 4=(2)^2

so we need 2 bits

192.168.0.0
192.168.64.0
192.168.128.0
192.168.192.0


### Configuring the router

we enter privilage exec mode using en command 
`en`

to show ip address use the following command
```bash
R1# sh ip int brief
Interface IP-Address OK? Method Status Protocol

GigabitEthernet0/0/0 unassigned YES unset administratively down down

GigabitEthernet0/0/1 unassigned YES unset administratively down down

Serial0/1/0 unassigned YES unset administratively down down

Serial0/1/1 unassigned YES unset administratively down down

Loopback0 1.1.1.1 YES manual up up

Vlan1 unassigned YES unset administratively down down

R1#conf t

Enter configuration commands, one per line. End with CNTL/Z.
```


now select the interface using `int`  command 
`int g0/0/0`

set the router in no shut mode so it never shuts down 

`no shut`

set the ip address for the interface

```
R1(config-if)#ip address 192.168.1.62 255.255.255.192

R1(config-if)#end

```
end command is used to exit priv mode


now we can check if the router is configured properly using 

```
  

R1#sh ip int brief

Interface IP-Address OK? Method Status Protocol

GigabitEthernet0/0/0 192.168.1.62 YES manual up up

GigabitEthernet0/0/1 unassigned YES unset administratively down down

Serial0/1/0 unassigned YES unset administratively down down

Serial0/1/1 unassigned YES unset administratively down down

Loopback0 1.1.1.1 YES manual up up

Vlan1 unassigned YES unset administratively down down

R1#ping 192.168.1.62

  

Type escape sequence to abort.

Sending 5, 100-byte ICMP Echos to 192.168.1.62, timeout is 2 seconds:

!!!!!

Success rate is 100 percent (5/5), round-trip min/avg/max = 0/4/9 ms
```


[[First Hop Redundancy protocols]]
