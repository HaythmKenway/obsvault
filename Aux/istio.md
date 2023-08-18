---
tags: k8s
---

Services mesh and istio

### What is istio?

service mesh manages communication between microservices
 
![[Pasted image 20230701151811.png]]

The main application needs to perform all the tasks including bl comm ..., so it would be a better solution if we have a sidecar application to perform all the tasks and the main application only works on the business logic

A service mesh has a control plane which automatically deploys the proxy and in every microservice so that microservices can talk to each other using the proxy

![[Pasted image 20230701152421.png]]

 ![[Pasted image 20230701154248.png]]
![[Pasted image 20230701154308.png]]

### Istio can be configured with k8s YAML files

There are Two main services to build the istio configuration
Virtual service 
Destination rule
![[Pasted image 20230701154425.png]]
![[Pasted image 20230701154534.png]]
![[Pasted image 20230701154542.png]]

We create crd's which are custom resource definitions in kubernetes

istiod converts these high level routing rules into Envoy-specific configurations

configuration is propagated into proxy sidecars

so we dont configure proxies we configure istiod
proxies can communicate without connecting to istiod
![[Pasted image 20230701154955.png]]


![[Pasted image 20230701155037.png]]

Setting up istio in k8's

for setup we can use simple kubernetes manifest provided by google
which can be downloaded by using the following

```bash

wget https://raw.githubusercontent.com/GoogleCloudPlatform/microservices-demo/main/release/kubernetes-manifests.yaml
kubectl  apply -f kubernetes-manifests.yaml 
kubectl get pods
watch kubectl get pods

```

After we deploy istios into our kubernetes cluster we can see our envoy proxies are not injected

First we setup a kubernetes cluster with 8 cpus and 8192 mb of memory
```
minikube start --cpus 8 --memory 8192

```

to install istiod into your cluster type 
```
istioctl istall
```

rename the default namespace to istio-injection=enabled
```
kubectl label namespace default istio-injection=enabled
```
create a deployment and apply the deployment to kubernetes and watch until the pods are ready
```
kubectl apply -f kubernetes-manifest.yaml
watch kubectl get pods
```

![[Pasted image 20230701232216.png]]

to monitor the pod using prometheus we can use the addons provided in the istio package

portforward prometheus to view it on the browser

```
kubectl apply -f /opt/istio/samples/addons/prometheus.yaml
kubectl -n istio-system port-forward prometheus-67f6764db9-jp2gh 9090


```

![[Pasted image 20230701232748.png]]


