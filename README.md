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

- difference between K8s, Docker Swarm, Puppet, Chef, Ansible
- Ingress
- Look into setting up katacoda so you can have kubectl running correctly on both nodes. That way you can watch pods in one node and send commands in the other.

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

We're going to start working with a Kubernetes cluster using Katacoda: https://www.katacoda.com/courses/kubernetes/playground

Katacoda provides a very simple cluster with one master node and one worker node.

## kubectl

`kubectl` is the command line tool that we use to communicate with a Kubernetes cluster.

```
$ kubectl get nodes
NAME      STATUS    ROLES     AGE       VERSION
master    Ready     master    9m        v1.10.0
node01    Ready     <none>    8m        v1.10.0
```

```
$ kubectl get pods
No resources found.
```

```
$ kubectl get componentstatus
NAME                 STATUS    MESSAGE              ERROR
scheduler            Healthy   ok
controller-manager   Healthy   ok
etcd-0               Healthy   {"health": "true"}
```

```
$ kubectl get pods -n kube-system -o wide
NAME                             READY     STATUS    RESTARTS   AGE       IP            NODE
etcd-master                      1/1       Running   0          17m       172.17.0.68   master
kube-apiserver-master            1/1       Running   0          17m       172.17.0.68   master
kube-controller-manager-master   1/1       Running   0          17m       172.17.0.68   master
kube-dns-86f4d74b45-pkgtz        3/3       Running   0          18m       10.32.0.2     node01
kube-proxy-hjwkz                 1/1       Running   0          18m       172.17.0.68   master
kube-proxy-np45k                 1/1       Running   0          18m       172.17.0.73   node01
kube-scheduler-master            1/1       Running   0          17m       172.17.0.68   master
weave-net-5rltx                  2/2       Running   1          18m       172.17.0.68   master
weave-net-xpcr7                  2/2       Running   0          18m       172.17.0.73   node01
```



## Deploying a Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kuard
spec: 
  containers:
    - image: gcr.io/kuar-demo/kuard-amd64:1
      name: kuard
      ports:
        - containerPort: 8080
          name: http
          protocol: TCP
```

```
$ kubectl apply -f pod.yml
```

(Show other statuses on the way to running?)

```
$ kubectl get pods
NAME                    READY     STATUS    RESTARTS   AGE
kuar-7595678cdf-57ccf   1/1       Running   0          6s
```

```
$ kubectl delete pods/kuard
```

```
$ kubectl delete -f pod.yml
```

### Resource requests

### Health checks

### Labels and Annotations

## Current and Desired State

```
kubectl run kuar --image=gcr.io/kuar-demo/kuard-amd64:1 -r 3
kubectl get pods
kubectl delete pod/kuar-7595678cdf-8dxr8
kubectl get pods
```

## Services



## Cascading API objects

## ReplicaSets

## Deployments

## ConfigMaps and Secrets

## Storage
