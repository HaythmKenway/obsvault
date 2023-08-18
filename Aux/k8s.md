---
tags: k8s

---
other reference:
[[Aux/Envoy]]
[[Prometheus]]
[[Service Mesh]]
[[istio]]


it is used to orchestrate docker containers

### What problems does kubernetes solve?
trend for monolith to microservices arcitecture

### Features of kuberneties?
High availablity
scalablity
Disaster recovery

---
### Pod 
smallest unit of k8
Abstraction over container
usually 1 application per pod
each pod has its own ip address

pods can die very easily  on each restart they are assigned new ip's so to avoid this we can use services and ingress

----

### Service and ingress
+ services is a permanent ip address which can be attached to its own pod
+ lifecycle of pod and services are not connected
There are two types of services 
External and internal services
External services can be accessed by outside the world but internal services can be only acessed within the access level

### Ingress 
In Kubernetes (K8s), an Ingress is an API object that manages external access to services running within a cluster. It provides a way to configure and manage inbound network traffic, typically for HTTP and HTTPS protocols, to route requests to the appropriate services based on rules defined by the user.

An Ingress acts as a traffic controller or entry point to the cluster, allowing external users or systems to access services running inside the Kubernetes cluster. It abstracts the complexity of routing and load balancing from the underlying services, making it easier to manage external access and routing rules.

Ingress resources define a set of rules that specify how incoming requests should be routed. These rules can be based on the requested hostname, path, or other HTTP headers. Depending on the specified rules, Ingress can direct traffic to different services or even different paths within the same service.

To enable Ingress functionality, a Kubernetes cluster needs to have an Ingress controller deployed. The Ingress controller is responsible for implementing the actual traffic routing and load balancing based on the Ingress rules. There are different Ingress controllers available for Kubernetes, such as Nginx Ingress Controller, Traefik, or HAProxy Ingress.

By using Ingress, you can expose multiple services over a single IP address, share the same TLS certificate for HTTPS encryption, and apply fine-grained routing rules for different endpoints within your cluster.

Overall, Ingress in Kubernetes provides a flexible and scalable approach to managing external access and routing within a cluster, allowing for more efficient and controlled traffic flow.

----

### important notes

pods communicate with each others using services

---
### ConfigMap:-
it is an external configuration to the config file of the application
it contains configuration data of the application wwe can simply connect it to a pod and 
![[Pasted image 20230614193424.png]]

### SECRET
secret is used to store secret data
it stores data in base64 format 
it usually contains credentials,certificates etc
it is connected to pod like configmap
we can use environmental variables to get the variables of configmap and secrets or as a properties files

---

# Volumes

  database of pods are usually non persistent so when the pod is restarted the data in the pod is forever gone 
  so the way to maintain persistence is using volumes
  ![[Pasted image 20230614194753.png]]

### Deployment and Stateful sets

there may be chances we need to restart the pod, or pod may crash which can cause downtime ,
since we are in an distributed environment so we can spawn more no of pods as necessary

we can define blueprints for pods we wwould like to  run and it is called BLUEPRINT

![[Pasted image 20230614203429.png]]

we may think what happens if database pod dies
we cant replicate database pods coz they have states they have same shared store .

Hence we use
### StatefulSet
deployments for database should be done using statefulsets 
it maintains synchronisation with database so there are no inconsistencies

Since maintaining databases among kubernetes is hard we actually dont use it , hence it is adviced to use databases outside of k8's cluster

----

### Kubernetes Architecture

kubernetes follows master slave arch


#### Node processing

each node has multiple pods on it
3 processes must be installed on every node
worker nodes do thew actual node

first process here is container runtime

kubelet interacts with both the container and node
kubelet starts the pod with a container inside

communication is done via services 

k8s cluster consists of multiple nodes which consists of container runtimes, kubelets and proxies

the third process is kube proxy 

kube proxy must be installed in all nodes
 

---

## Master node


How do you interact with this cluster??
Managing processes are done by master nodes


There are usually 4 services installed in the master process

1. api server:  it is a cluster gateway which gets the request and it also acts as authentication gateway
![[Pasted image 20230615201449.png]]
since we have 1 entry point to request it enhances security

2. Scheduler
Scheduler  starts the process of the pod in one of the node
it looks into resources of worker node and assigns pods to node
![[Pasted image 20230615204851.png]]

3. Controller manager

it detects state changes like pod dead state
![[Pasted image 20230615204955.png]]

it uses scheduler and assigns the pods to new

4 etcd
![[Pasted image 20230615205124.png]]

----

### creating pods

we cannot create pods directly in kubernetes so we create deployments

![[Pasted image 20230616032248.png]]


Creating deployment

`kubectl create deployment NAME --image=IMAGE [--dry-run][options]`

getting deployment and pod info

![[Pasted image 20230616032522.png]]

editing a deployment

`kubect edit deployment <name>`

Getting logs

`kubectl logs <deployment>`

TO execcute pod

`kubectl exec -it <deployment>

To Delete deploymennt
`kubectl delete deployment <name>`

To create and apply configurations

`kubectl apply -f Config"`

---
configuring k8's

COnfiguration file have 3 parts
1) metadata
2) specification
3) status 


---
## Minikube

Minikube is a test/local cluster setup which comes with a docker container envronment preinstalled 

### Kubectl

in order to interact with the containers we need ui,api or cli which so we use a cli tool called cubectl to controll kubernetes cluster


![[Pasted image 20230627192535.png]]


starting minikube

to start minikube we can use the following command 

`minikube start --vm-driver=qemu2`

![[Pasted image 20230627193635.png]]

To get all the list of running nodes we use the following command

![[Pasted image 20230627193710.png]]

we use kubectl cli for configuring the cluster

minikube cli for startup/deleting cluster


---
### Basic Kubectl commands

to get the names of nodes, pods and services
![[Pasted image 20230627200028.png]]

1. Nodes: A node, also known as a worker node or a minion, is a physical or virtual machine that forms part of a Kubernetes cluster. It is responsible for running containers and executing workloads. Nodes are where your applications are deployed and run. They provide the necessary resources (CPU, memory, storage) to host and execute containers.
    
2. Pods: A pod is the smallest and simplest unit in the Kubernetes object model. It represents a single instance of a running process or workload within the cluster. A pod can contain one or more tightly coupled containers that share the same resources, network, and storage. These containers are scheduled and deployed together on the same node. Pods are used to encapsulate and manage the lifecycle of the containers, providing a cohesive environment for application components.
    
3. Services: A service is an abstraction that defines a logical set of pods and a policy to access them. It acts as a stable network endpoint to facilitate communication between different components of an application or between applications themselves. Services enable load balancing and service discovery within the Kubernetes cluster. They can be exposed internally within the cluster or externally to the outside world, allowing access to applications running in pods. Services typically provide a reliable DNS name or IP address that can be used by other services or external clients to connect to the pods.


---
In kubernetes we actually dont create pods we create deployments

### Replicasets

In Kubernetes, a ReplicaSet is a higher-level abstraction that ensures a specified number of pod replicas are running at all times. It is a controller that helps in maintaining the desired state of a set of pods.


we have created a deployment with the following command
![[Pasted image 20230627202731.png]]

then we can use get command to get information about deployment pods and replicasets

![[Pasted image 20230627202539.png]]


Layers of abstraction

![[Pasted image 20230627202912.png]]


### Editing Deployment

![[Pasted image 20230627203059.png]]

so we can see that as we made our edits a new replicaset has been created 
![[Pasted image 20230627203307.png]]

#### to get logs
![[Pasted image 20230627204009.png]]

To create and apply configuration file

`kubectl apply -f <file.yaml>`

![[Pasted image 20230627211036.png]]
![[Pasted image 20230627211057.png]]

---

## MInikube configuration file

Each configuration files have 3 parts 
1) metadata 
2) specs
3) status

metadata generally contains name and other specific details about the deployment

specs contains specifications 
specs are specific to the kind


Status is automatically updated in k8's and if the cluster is not running in the expected format then the k8s orchestrates the containers as expected

The status data comes from the cluster brain etcd

![[Pasted image 20230627214122.png]]

port is the port no of pod 
and target port is the service for which the service traffic is routed to

[[Creating a complete k8s setup]]

### Namespaces
namespaces are used to seperate components form different components of the kubernetes environemnt

service is the only resource which can be shared across namespaces 
all other resources of the namespaces are slef contained

![[Pasted image 20230628072426.png]]

we use `<namespace>.<component>` notation to share components across namespaces

There are some components in k8's which are non namespaced
for example we have nodes and volumes which cannot be contained in a namespace

#### creating components using namespace
if we dont provide a namespace to a component it iis initialized in the default namespace

we can include the namespace in the metadata tag of the config file or we can explicitly add it while configuring the namespace


----

#### ingress

What is ingress
for external app to reach your application we can use external 
by opening the port

insted we can use an internal service  named ingress to send the data from the client to an internal service 

we use a loadbalancer and assign a public address as an ip to the pod and expose it to the network

![[Pasted image 20230628074516.png]]



### Example for ingress
![[Pasted image 20230628074636.png]]


host is the host specified  and path is the value present after the host in the url



### Helm

it is a package management for kubernetes
it is a templating engine

### Kubernetes volume
1) persistent volume
2) persistent volume claim
3) Storage class

![[Pasted image 20230628094428.png]]

There are 2 types of volume Local and Remote


Storage class creates persistent volumes dynamically in the background 


### Services in kubernetes

pods in kubes are ephemeral 
![[Pasted image 20230628100416.png]]


There are several type 


pods are identified using selectors and these contains a set of key value pairs
labels of pods  are present 

### Cluster ip

the http request hits the ingress and ingress forwards the request to the service node, which inturn trasnsfers the request to the worker nodes 
this internal service node is called selector

whenever we create a service an service endpoint is created

service port is arbitary but target ip must match a node in one of the worker nodes 


### Headless Server

it makes the application too tied to API
its inefficient


### NOdeport
nodeport can be accessed from external services