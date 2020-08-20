# Kubernetes-Lab
## Tips
- [kubectl CheatSheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- [kubectl Usage Conventions](https://kubernetes.io/docs/reference/kubectl/conventions/)
## Basics
#### Lab 1: PODs
See details of this lab via [Pods](https://github.com/juliehub/Kubernetes-Lab/blob/master/Lab1-Pods.md)
##### Important Commands for lab 1:
  - Download [pod-definition.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/pod-definition.yml)
  - Run commands:
  ```bash
  $ kubectl create -f pod-definition.yml
  $ kubectl run nginx --image nginx
  $ kubectl get pods
  $ kubectl describe pod newpods-4rtwk 
  $ kubectl get pods -o wide
  $ kubectl delete pod webapp
  $ kubectl run redis --image=redis123 --dry-run=client -o yaml > pod.yaml
  $ kubectl apply -f pod.yaml
  $ kubectl edit pod redis
  ```
#### Lab 2: ReplicaSet
See details of this lab via [ReplicaSets](https://github.com/juliehub/Kubernetes-Lab/blob/master/Lab2-ReplicaSets.md)
##### Important Commands for lab 2:
  - Download [replicaset-definition.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/replicaset-definition.yml) and [compute-quota.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/compute-quota.yml)
  - Run commands:
  ```bash
  $ kubectl create -f replicaset-definition.yml
  $ kubectl get replicatset
  $ kubectl get pods
  $ kubectl get all
  $ kubectl delete replicaset myapp-replicaset
  ```
  Scale with 6 replicas
  ```bash
  $ kubectl replace -f replicaset-definition.yml
  $ kubectl scale --replicas=6 -f replicaset-definition.yml
  $ kubectl scale --replicas=6 replicaset myapp-replicaset
  ```
#### Lab 3: Deployments
See details of this lab via [Deployments](https://github.com/juliehub/Kubernetes-Lab/blob/master/Lab3-Deployments.md)
##### Important Commands for lab 3:
  - Download [deployment-definition.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/deployment-definition.yml)
  - Run commands:
  ```bash
  $ kubectl create -f deployment-definition.yml
  $ kubectl get deployments
  $ kubectl get replicatset
  $ kubectl get pods
  $ kubectl get all
  ```
##### Tips for lab 3
- Create an NGINX Pod

`kubectl run --generator=run-pod/v1 nginx --image=nginx`
- Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)

`kubectl run --generator=run-pod/v1 nginx --image=nginx --dry-run -o yaml`
- Create a deployment

`kubectl create deployment --image=nginx nginx`
- Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

`kubectl create deployment --image=nginx nginx --dry-run -o yaml`
- Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)

`kubectl create deployment --image=nginx nginx --dry-run -o yaml > nginx-deployment.yaml`

- Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.

#### Lab 4: NameSpaces
See details of this lab via [Namespaces](https://github.com/juliehub/Kubernetes-Lab/blob/master/Lab4-NameSpaces.md)
##### Important Commands for lab 4:
- Download [namespace-dev.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/namespace-dev.yml)
- Run commands:
 ```bash
 $ kubectl get ns
 $ kubectl get pods --namespace=kube-system
 $ kubectl create -f pod-definition.yml --namespace=dev
 $ kubectl create namespace dev
 $ kubectl create -f namespace-dev.yml
```
- Switch namespace
```bash
 $ kubectl config set-context $(kubect config current-context) --namespace=dev
 $ kubectl get pods
 $ kubectl get pods --namespace=default
 $ kubectl get pods --namespace=prod
 $ kubectl get pods --all-namespaces
```
- Create quota
```bash
$ kubectl create -f compute-quota.yml
```
#### Lab 5: Services
See details of this lab via [Services](https://github.com/juliehub/Kubernetes-Lab/blob/master/Lab5-Services.md)
##### Important Commands for lab 5:
- Download [service-definition.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/service-definition.yml)
- Download [service-clusterIP-definition.yml](https://github.com/juliehub/Kubernetes-Lab/blob/master/service-clusterIP-definition.yml)
- Run commands:
```bash
$ kubectl create -f service-definition.yml
$ kubectl get services
```
- Access the Node port using `curl http://192.168.1.2:30008`

