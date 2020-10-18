# Multi container application with k8s

## List of elements
* PersistentVolumeClaim type
    * database-persistent-volume-claim
* Deployment
    * postgres-deployment
    * redis-deployment
    * server-deployment
* Service
    * postgres-cluster-ip-service
    * redis-cluster-ip-service
    * server-cluster-ip-service

## Graph of elements
```mermaid
graph LR
A(database-persistent-volume-claim) -- used by --> B(postgres-deployment <br> postgres:13.0)
B -- exposed by --> C[postgres-cluster-ip-service <br> postgres:5432]
D(redis-deployment <br> redis:6.0.8) -- exposed by --> E(redis-cluster-ip-service <br> redis:6379)
F(server-deployment <br> brockmarekins/multi-k8s-server:latest) -- exposed by --> G(server-cluster-ip-service <br> server:5000)
C -- used by --> G
E -- used by --> G
```
