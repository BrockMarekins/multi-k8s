# Multi container application with k8s

## List of elements
* PersistentVolumeClaim type
    * database-persistent-volume-claim
* Deployment
    * postgres-deployment
    * redis-deployment
* Service
    * postgres-cluster-ip-service
    * redis-cluster-ip-service

## Graph of elements
```mermaid
graph LR
A(database-persistent-volume-claim) -- used by --> B(postgres-deployment)
B -- exposed by --> C[postgres-cluster-ip-service]
D(redis-deployment) -- exposed by --> E(redis-cluster-ip-service)
```
