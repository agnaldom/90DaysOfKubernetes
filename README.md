# CKA

## Cluster Architecture

### Kubernetes Architecture

### ETCD for Beginners

ETCD is a distributed reliable key-value store that is Simple, 
Secure & Fast

* Install ETC
    1.  Download Binaries
    2.  Extract
    3.  Run ETCD Service

For default ETCD run in port 2379

### ETCD in Kubernetes

* ETCD CLUSTER
    * Nodes
    * PODs
    * Configs
    * Secret
    * Accounts 
    * Roles
    * Bindings
    * Others

Explore ETCD
* Registry  - minions
            - pods
            - replicasets
            - deployments
            - roles
            - secrets

### Kube-API Serve

1.  Authenticate User
2.  Validate Request
3.  Retrive data
4.  Update ETCD
5.  Scheduler
6.  Kubelet

### Controller Managers

* Watch Status
* Remediate Situation
* Node Monitor Period = 5s
* Node Monitor Grace Period = 40s
* POD Eviction Timeout = 5m

### Kuber Scheduler

1.  Filter Nodes
2.  Rank Nodes

More Later..

* Resource Requirements and Limits
* Taints and Tolerations
* Node Selectors/Affinity

### Kubelet

* Register Node
* Create PODs
* Monitor Node & PODs

### Kube Proxy