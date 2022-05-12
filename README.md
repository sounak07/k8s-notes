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

[More info](https://www.youtube.com/watch?v=OW244LxB4oI)

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


### Local Demo App

`Note: Order of creation matters !`

- Create Secret config file 
- Apply secret config file
- Create mongo-db deployment

![alt text](/resources/secret.png "sfs")


### Namespaces 

- Can be used to group together different types of services/resources
- Two teams using same clusters , namespace are useful
- Can be used to deploy staging and dev using common services like ELK or nginx-ingress
- Can be used in blue Green/blue deployments using common services like ELK or nginx-ingress
- Limiting resource to a particular namespace
- ConfigMap and secrets are restricted to namespaces
- Service can be shared across namespaces

`Note: Use kubens to change your default namespace`

#### How to create a resource with a namespace

![alt text](/resources/namespace.png "sfs")


### K8s Ingress

- Inorder to use ingress we will create a internal controller. Requests on ingress will be directed to internal service which will eventually reach pods.

![alt text](/resources/ingress.png "sfs")
![alt text](/resources/ingress2.png "sfs")

Steps:

- Install ingress Controller on minikube
- Create ingress rules
- Add hosts and IP in /etc/hosts

`Requests -> minikube -> ALB/Nginx (Imp. for prod) -> Ingress Controller -> Ingress Rules -> Service`

![alt text](/resources/ingress3.png "ing")
![alt text](/resources/ingress4.png "ing")
![alt text](/resources/ingress5.png "ing")

#### TLS in Ingress

![alt text](/resources/tlsingress.png "ing")
![alt text](/resources/tlsingress2.png "ing")


### Helm k8s

![alt text](/resources/helm.png "ing")
![alt text](/resources/helm2.png "ing")
![alt text](/resources/helm3.png "ing")
![alt text](/resources/helm4.png "ing")
![alt text](/resources/helm5.png "ing")
![alt text](/resources/helm6.png "ing")
![alt text](/resources/helm7.png "ing")

```
helm install <chartname> -n [namespace] [helm-chart-folder] --dry-run
helm upgrade <chartname>
helm rollback <chartname>
helm list -n [namespace]
```
- Tiller isn't there anymore as it has too much permissions which makes it a secuirity issue.It has been deprecated in Helm 3

[More info](https://www.youtube.com/watch?v=YDZ_i6OhjhQ&t=182s)

```
Notes:

Helm will kind of help us with dynamic values that will be picked up from values.yaml or from cli using --set 

```

### Volumes in K8s

![alt text](/resources/vol1.png "vol")
![alt text](/resources/vol2.png "vol")
![alt text](/resources/vol3.png "vol")
![alt text](/resources/vol4.png "vol")
![alt text](/resources/vol5.png "vol")

- Admin creates storage resource -> User claims for pvc -> Attach to POD -> containers
- Multiple types of volumes can be mounted to pods like config map files, vol etc
- Storage class can be used to create persistent volume clusters


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
 - kubectl delete -f [config-file.yaml] // to delete yaml file and service/deployment
 - kubectl get deployment nginx-deployment -o yaml > nginx-result.yml // gets detailed config
 - kubectl get ns  // get all namespaces
 - kubectl get ingress -n [namespace]
 - kubectl describe ingress [ingress-name] -n [namespace]  // to display ingress backend
 - kubectl get all -n [namespace]  // to get all details about a namespace

```

### Resouces

[Kubernetes Playlist](https://www.youtube.com/playlist?list=PLh4KH3LtJvRRcSwTZgmW60lkhVrzKU1jA)



