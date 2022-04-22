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




