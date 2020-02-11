# Controllers

## [Official reference](https://kubernetes.io/docs/concepts/workloads/controllers)

## ReplicationController / ReplicaSet

{% embed url="https://www.youtube.com/watch?v=1As1CPuyTao" %}

## Deployments

> A _Deployment_ provides declarative updates for [Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) and [ReplicaSets](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).
>
> You describe a _desired state_ in a Deployment, and the Deployment [Controller](https://kubernetes.io/docs/concepts/architecture/controller/) changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

## StatefulSets

> StatefulSet is the workload API object used to manage stateful applications.
>
> Manages the deployment and scaling of a set of [Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/) , _and provides guarantees about the ordering and uniqueness_ of these Pods.
>
> Like a [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) , a StatefulSet manages Pods that are based on an identical container spec. Unlike a Deployment, a StatefulSet maintains a sticky identity for each of their Pods. These pods are created from the same spec, but are not interchangeable: each has a persistent identifier that it maintains across any rescheduling.

## DaemonSet

> A _DaemonSet_ ensures that all \(or some\) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.
>
> Some typical uses of a DaemonSet are:

## Garbage Collection

## TTL Controller for Finished Resources

## Jobs - Run to Completion

## CronJob



