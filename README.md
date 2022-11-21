# Optimizing Workload and Compute in Kubernetes

### About me
https://arslanali.io


Binding and placement of pending Pods on to respective nodes are managed by a scheduler in kubernetes called kube-scheduler. The placement decision are often managed by configurable scheduling policies and rules, often called as predicates and priorities. The desicion of a scheduler is based on the actual condition/state of the Cluster at the time when the Pod is requested to be deployed. Since the Kubernetes cluster may change its state by update/change of labels, taints, tolerations or even by introducing new nodes into it. There may be a desire of relocating a pod from one node to another, a.k.a descheduler.

## When do you need a Descheduler
There could be a number of scenarios when you may want to deschedule (evict) a Pod from a node, lets discuss some of them:

### 1. New node is introduced in a cluster  
You have just introduced a new node in the cluster and want to distribute the workload evenly.

### 2. Node labels/tainsts/afiniity are updated  
Pod and node affinity requirements, such as taints or labels, have changed and the original scheduling decisions are no longer appropriate for certain nodes.

### 3. Node failure require Pods to be moved  
Pods are in stale condition (readiness and health probes are returning errors) on a failed Node, manual eviction is required.

### 4. You want to remove Duplicates
Similar pods are running on a single node. 

### 5. Low Node Utilization
A 20% or less CPU/Mem is reserved then it is considered as low utlization of a node. You may want to deschedule its Pods and killing it all together.

### 6. High Node Utilization  
A 20% or less CPU/Mem is reserved then it is considered as low utlization of a node. You may want to deschedule its Pods once a new node is added to share the load.

### 7. Pods Violating Inter Pod AntiAffinity  
You want to Remove Pods Violating Inter Pod AntiAffinity
### 8. Pods Violating Node Affinity  
You may also want to Remove Pods Violating Node Affinity
### 9. Pods Violating Node Taints  
Remove Pods Violating Node Taints  
### 10. Pods Violating Topology Spread Constraint
Remove Pods Violating Topology Spread Constraint
### 11. Pods Having Too Many Restarts
Remove Pods Having Too Many Restarts, as it may be because of underlying Node Taints, Resources available etc.
### 12. Pod LifeTime is achieved  
Remove Pods that are too old, lifetime requirements can be configured using descheduling policy.
### 13. Remove Failed Pods  
Pods have been restarted may times.



## Options of Available Deschedulers
The descheduler is not a native Kubernetes service, which is why there are multiple options available in both licensed and opensource communities
1. Openshift Descheduler
2. Open Source Deschedulers
3. Cloud Provider Market Places
4. SaaS Providers (e.g: Kaiops.io)


## Demo (Using Opensource Rule based Descheduler)
I have setup a basic cluster with a few nodes and some sample workload running on them. We will use a few scenarios to observe the behavior of the cluster with/without the descheduler services.

1. Add a new Node
2. Remove Pod Duplicates
3. Node afinity updated using taints and labels.
