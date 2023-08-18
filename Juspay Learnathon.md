### Hackathon docs walk through

first we have been provided with files to deploy within the kubernetes cluster and we have to perform the following things in order


#### Task 0

Execute the following commands in order
```
  kind create cluster --config k8s/cluster/kind-cluster-config.yaml 
  kubectl cluster-info --context kind-kind
  kubectl get no --context kind-kind
  ./scripts/build-docker.sh  
  kubectl apply -f k8s/configs/pinger-all-in-one.yaml 
  kubectl get deploy
```

### Task 1

#### Activity 1

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
echo -n 'adminuser' > ./admin-user # change your username
echo -n 'p@ssword!' > ./admin-password # change your password
 kubectl create secret generic grafana-admin-credentials --from-file=./admin-user --from-file=admin-password 
kubectl describe secret grafana-admin-credentials
rm admin-user && rm admin-password
curl https://raw.githubusercontent.com/techno-tim/launchpad/master/kubernetes/kube-prometheus-stack/values.yml -o k8s/configs/values.yaml
helm install prometheus prometheus-community/kube-prometheus-stack -f k8s/configs/values.yaml
kubectl port-forward  grafana-fcc55c57f-fhjfr 52222:3000

```

### Tasks using istio

```
 kind create cluster --config k8s/cluster/kind-cluster-config.yaml 
  kubectl cluster-info --context kind-kind
  kubectl get no --context kind-kind
  ./scripts/build-docker.sh  
  kubectl apply -f k8s/configs/pinger-all-in-one.yaml 
  kubectl get deploy
  
```