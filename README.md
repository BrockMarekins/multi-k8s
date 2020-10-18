# Multi container application with k8s

## List of elements
* PersistentVolumeClaim
    * database-persistent-volume-claim
* Deployment
    * postgres-deployment
    * redis-deployment
    * server-deployment
    * client-deployment
* Service
    * postgres-cluster-ip-service
    * redis-cluster-ip-service
    * server-cluster-ip-service
    * client-cluster-ip-service
* Ingress
    * ingress-service

## Graphs of dependencies

### postgres dependencies
```mermaid
graph LR
A(database-persistent-volume-claim)
B(postgres-deployment <br> postgres:13.0) 
C(postgres-cluster-ip-service <br> postgres:5432)

A -- used by --> B
B -- exposed by --> C
```

### redis dependencies
```mermaid
graph LR
A(redis-deployment <br> redis:6.0.8) 
B(redis-cluster-ip-service <br> redis:6379)

A -- exposed by --> B
```

### server dependencies
```mermaid
graph LR
A(server-deployment <br> brockmarekins/multi-k8s-server:latest)
B(server-cluster-ip-service <br> server:5000)

A -- exposed by --> B
```

### client dependencies
```mermaid
graph LR
A(client-deployment <br> brockmarekins/multi-k8s-client:latest)
B(client-cluster-ip-service <br> client:3000)

A -- exposed by --> B
```

### ingress dependencies
```mermaid
graph LR
A(server-cluster-ip-service <br> server:5000)
B(client-cluster-ip-service <br> client:3000)
C(ingress-service)

A -- exposed by --> C
B -- exposed by --> C
```

### application dependencies
```mermaid
graph LR
A(postgres:5432) 
B(redis:6379)
C(server:5000)
D(client:3000)
E(ingress-service)

A -- used by --> C
B -- used by --> C
C -- used by --> D
C -- exposed by --> E
D -- exposed by --> E
```
