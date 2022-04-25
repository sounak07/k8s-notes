# KUBERNETES

 - [Major Components of K8s](#major-components-of-k8s)
 - [Kubernetes Architecture](#kubernetes-architecture)

## Major Components of k8s

![alt text](/resources/k8Comps.png "k8")

- [PODs](#pods)
- [Service](#service)
- [ConfigMap](#configmap)
- [Secrets](#secrets)
- [ConfigMap](#configmap)
- [Deployments in K8s](#deployments)
- [StateFULSets in K8s](#statefulset)


### PODs
#

![alt text](/resources/k8s-pod.png "k8")

- A layer/abstraction over containers so as to allow replacing of containers

### Service
#

![alt text](/resources/k8s-service.png "k8")
![alt text](/resources/k8s-service2.png "k8")

- Ingress is used for creating user friendly domain
- Request is directed to ingress which forwards the request to service

![alt text](/resources/k8-service3.png "k8")


### ConfigMap
#
![alt text](/resources/configMap.png "configMap")

- Its like env to where we can pass configurations of an applications like name etc.

### Secrets
#
![alt text](/resources/configMapsecret.png "secret")

- Just like configMap but for secrets like passwords, etc.

### Databases in k8s
#
 - Volumes can be attached to k8s in order to maintain data persistance.
 - k8s doesn't maintain data persistance

### Deployments
#
- A blue print to define number of replicas you would want to run. Scale up/ scale down is also possible. Limited to stateless services.
- Databases can't be replicated.

![alt text](/resources/deployments.png "dep")

### StatefulSet
#
![alt text](/resources/statefulsets.png "sfs")

- Replications stateful services like dbs
- Deployments are for StateLESS Apps vs StatefulSets are for StateFUL Apps 
- Deploying with StateFULSets is difficult. Common practice is to deploy DBs outside of K8s.  


![alt text](/resources/overall.png "sfs")

- Replications allows high availability


## Kubernetes Architecture

### Kubelets and Kube Proxy
#
![alt text](/resources/kubelets.png "sfs")

- Kubelets interacts with both the container and the node
- Kubelet starts the pod with a container inside

![alt text](/resources/k8s-Arch.png "sfs")

- Kube Proxy forwards the requests caught by services to their respective pods.
- Intelligent logic to forwards the request to originating from a pod to a service running in same pod as shown above. 


### Master Nodes Architector
#
#### Api Server

![alt text](/resources/k8s-arch2.png "sfs")

#### Scheduler
![alt text](/resources/k8s-arch-sceduler.png "sfs")

- Scheduler checks for resourse usage by for Node and schedule the new pod as per usage.
- Schedule decides the node while kubelet starts the new pod in that decided node.

#### Controller Manager

![alt text](/resources/k8s-arch-controller.png "sfs")

- When a pod dies/crashes, controller Manager detects these state changes and calls the scheduler.
- Scheduler checks for resourse usage by for Node and re-schedule the restart/new pod as per usage.

#### etcd ( key-val-> Cluster brain)

![alt text](/resources/k8s-arch-etcd.png "sfs")

- Cluster changes get stored in the key value store like resource availability , pods running, cluster health any other cluster states.

- Application data is NOT stored

``` 
Depending upon usage we can Add new nodes/master nodes.
Steps: 
    - Get a new bare server
    - install all the master / worker node processes
    - add it to the cluster
```


### Minikube
- A dev setup component where both master and worker nodes run in a single node for easy dev setup.

### Kubectl
- A command line client for kubernetes to interact with clusters of k8s.

### Installation

- Hyperkit
- kubectl
- Minikube

![alt text](/resources/abstraction.png "sfs")
### Commands

```bash
Start a k8 cluster -> minikube start --vm-driver=hyperkit
Minikube status -> minikube status
```

![alt text](/resources/basic-commands.png "sfs")
![alt text](/resources/basic-commands-2.png "sfs")

```
kubectl Commands : 

 - kubectl get nodes
 - kubectl get pod
 - kubectl get services
 - kubectl create deployment nginx-depl --image=image [dry-run] [other options]
 - kubectl get replicaset // To get a replica-set created automatically
 - kubectl edit deployment [deployment-name]
 - kubectl describe pod [pod-name]
 - kubectl logs [pod-name]
 - kubectl exec -it [pod-name] -- bin/bash
 - kubectl delete deployment [deployment-name] // delete a deployment
 - kubectl apply -f [config-file.yaml] // to apply/re-apply yaml file 
 - kubectl delete -f [config-file.yaml] // to delete yaml file 

```

### Kubernetes Config file

There are 3 parts in the config file:
- MetaData
- Specification
- Status 
    -> Automatically added by k8s which is used to track changes. Data is received by k8s from etcd


![alt text](/resources/config1.png "sfs")
![alt text](/resources/config2.png "sfs")

- Label is used to connect pods with deployments
- Service uses Label to make a connection with deployments and its pods.

![alt text](/resources/config3.png "sfs")




