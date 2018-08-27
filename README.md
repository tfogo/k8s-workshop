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

## Notes

- difference between K8s, Puppet, Chef, Ansible
- Ingress

## What is Kubernetes?

Kubernetes is an open-source sysyem for deploying, scaling, and managing applications using containers. The precursor to Kubernetes is Borg - Google's internal tool for cluster orchestration. In 2014 the open source version of Borg called Kubernetes was released. Since then, Kubernetes has gorwn immensely. It's a fast growing project with a very large ecosystem. The Kubernetes project is now stewarded by the Cloud Native Computing Foundation (which itself is a part of the Linux Foundation).

Kubernetes is the Greek for Helmsman or Pilot. That's why the logo is a ship's wheel (and you'll notice sialing terms and metaphors used a lot in Kubernetes products because of this). It is the root of the words Governer and Cybernetics. Often times we just call it K8s for short. In fact our smoothie mascot is called Kate in honour of Kubernetes!

### Containers - the modern way of development



## What is the value of Kubernetes?

## Kubernetes components

Kubernetes is made up of several components. It's useful to understand what these components are and what they do. Each component is it's own binary that needs to be set up and run on a node.

A Kubernetes cluster is made up of several machines. We have master nodes which manage the cluster and worker nodes where application containers are actually run. Some components of Kubernetes run on all nodes and some only run on master nodes.

### Master Components

#### etcd

The first thing we need is a database to store information about our cluster. Kubernetes uses a database called etcd, which is a distributed key/value store. Sometimes this is on its own nodes, often times it's on the same nodes as the rest of the master components.

#### kube-apiserver

This is a webserver that hosts the Kubernetes API. The Kubernetes API is the core of the Kubernetes system. Other components talk to each other through the API. The API is a JSON API that you can send requests to directly, but generally you will use the kubernetes CLI `kubectl`.

#### kube-scheduler

This components watches for containers that haven't been assigned to run on a node and selects a node for them to run on. The scheduler has to take many factors into account to decide where to run containers such as resource requirements, hardware contraints, and user-defined specifications.

#### kube-controller-manager

These are the core control loops of Kubernetes. The Kubernetes controller manager will constantly watch the state of the cluster and will make changes to move the current state of the cluster to the desired state. It observes and acts on the cluster through the API server.

#### cloud-controller-manager
***
These are cloud-specific control loops. Kubernetes has the built-in ability talk to several cloud providers. So if the cluster needs to spin up a load blanacer, Kubernetes will be able to do that whether it's on AWS, GCP, Azure, and more. The cloud controller manager can also manage third-party control loops.


### Node Components

These components run on every node.

#### Kubelet

The kubelet is the primary agent that runs on each node. It takes a list of pod specifications from the apiserver and ensures the containers described in that pod are running and healthy.

#### kube-proxy

A network proxy that runs on each node. Allows service discovery in Kubernetes so applications can easily talk to each other.

#### container runtime

You can choose the container runtime which will run your containers. You can use Docker, runc, rkt, or any OCI-compliant container runtime.

#### DNS

Kubernetes nodes require a DNS service to allow for service discovery. The default DNS is kube-dns, but CoreDNS is a newer alternative.

#### Pod networking

Your cluster must implement its netowrk in such a way as pods have unique IPs and can communicate directly to each other on the same network. This can be done with a flat routed network, with an overlay network, or some other mechanism. This may require extra configuration or processes on nodes.


### Extras

You may wish to add extra functionality to your cluster, such as monitoring, logging, or other technolgoy. Kubernetes is a very configurable and extensible system. There are infinite ways you could set up your cluster.


## Setting up your own Kubernetes cluster

You could set up all components yourself - but this is hard.

There are command line tools that can help - e.g. minikube, kops, kubespray, kubeadm, kube-up

But you can always just set up a hosted kubernetes cluster with GKE.

## kubectl



## Deploying a Pod

## Specs

## Services

## ReplicaSets

## Deployments

## ConfigMaps and Secrets

## Storage
