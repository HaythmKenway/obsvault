---
tags: k8s
---

## External svc vs ingress

a Ui application needed its request to be able to accessible by external ip address


 Insted of opening a port for external service we will have an internal service
 the request from browser reaches the ingress and internal service
  ![[Pasted image 20230703005206.png]]
  in external service we configure a load balancer and we eexpose the nodeport using which we can access the applcation

### Ingress
![[Pasted image 20230703005324.png]]

ingress contains rules in specs
it routes the request to the service

![[Pasted image 20230703005412.png]]

in the rules specified, we are forwarding all the request to the myapp-internal-service
the services are identified using the name in the metadata 

note:- hostname should be mapped to an ip address


### Configuring Ingress contoller

first we need an implementation for ingress controller which is ingress controller
![[Pasted image 20230703005732.png]]


![[Pasted image 20230703010012.png]]


