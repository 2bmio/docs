---
description: >-
  The Concepts section helps you learn about the parts of the Kubernetes system
  and the abstractions Kubernetes uses to represent your cluster , and helps you
  obtain a deeper understanding of how Kubern
---

# Concepts

### Overview <a id="overview"></a>

### Kubernetes objects <a id="kubernetes-objects"></a>

### Kubernetes Control Plane <a id="kubernetes-control-plane"></a>

> kubernetes control plane consist of the following **components** on controller nodes: 
>
> 1. kube-**apiserver**: **allow** user/srv/etc **ineract** with the cluster
> 2. **etcd**: clustes datastore, **keep** multples controllers in **sync**
> 3. kube-**scheduler**: **dealing** into the cluster to apply desired **state**
> 4. **kube-controller-manager**: **runs** a series of controllers that provide a wide range of **cluster functionality**.
> 5. **cloud-controller-manager**: **handles** interaction with underlying **cloud providers**.
>
> This **set of services** is the magic on k8s ecosystem with worker nodes and control nodes

#### Kubernetes Master <a id="kubernetes-master"></a>

#### Kubernetes Nodes <a id="kubernetes-nodes"></a>

