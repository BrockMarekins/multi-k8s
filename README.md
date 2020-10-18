# Multi container application with k8s

## List of elements
* PersistentVolumeClaim type
  * database-persistent-volume-claim

## Graph of elements
```mermaid
graph LR
A(database-persistent-volume-claim) -- used by --> B(postgres-deployment)
B -- exposed --> C[postgres-cluster-ip-service]
```
