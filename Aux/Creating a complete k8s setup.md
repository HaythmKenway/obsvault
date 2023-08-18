---
tags: k8s
---

first we create a basic mongo cluster configuration with 2 replica set using the following code

mongo
```yaml
apiVersion: apps/v1

kind: Deployment

metadata:

name: mongodb-deployment

labels:

app: mongodb

spec:

replicas: 1

selector:

matchLabels:

app: mongodb

template:

metadata:

labels:

app: mongodb

spec:

containers:

- name: mongodb

image: mongo:4.4.6

ports:

- containerPort: 27017

env:

- name: MONGO_INITDB_ROOT_USERNAME

valueFrom:

secretKeyRef:

name: mongodb-secret

key: mongo-root-username

- name: MONGO_INITDB_ROOT_PASSWORD

valueFrom:

secretKeyRef:

name: mongodb-secret

key: mongo-root-password
```

mongo-secret
```yaml
apiVersion: v1

kind: Secret

metadata:

name: mongodb-secret

type: Opaque

data:

mongo-root-username: dXNlcm5hbWU=

mongo-root-password: cGFzc3dvcmQ=
```

we first create a secret using  by applying mongo-secret and then create a cluster using mongo

```
kubectl apply -f mongo-secret.yaml
kubectl apply -f mongo.yaml
```

### Creating services

