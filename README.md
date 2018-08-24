# k8s-workshop

- What is Kubernetes?
- What is the value of Kubernetes?
- Kubernetes components
- kubectl
- Deploying a Pod
- Specs
- Services
- ReplicaSets
- Deployments
- ConfigMaps and Secrets
- Storage

## What is Kubernetes?

## What is the value of Kubernetes?

## Kubernetes components

Kubernetes is made up of several components. It's useful to understand what these components are and what they do.

A Kubernetes cluster is made up of several machines. We have master nodes which manage the cluster and worker nodes where application containers are actually run.

### Master

#### etcd

The first thing we need is a database to store information about our cluster. Kubernetes uses a database called etcd, which is a distributed key/value store. Sometimes this is on its own nodes, often times it's on the same nodes as the rest of the master components.

#### kube-apiserver

#### kube-scheduler

#### kube-controller-manager

#### cloud-controller-manager


### Worker

#### Kubelet

#### kube-proxy

#### container runtime

#### DNS

#### Network overlay



## kubectl

## Deploying a Pod

## Specs

## Services

## ReplicaSets

## Deployments

## ConfigMaps and Secrets

## Storage
