### Introduction

[Microk8s](https://microk8s.io/docs) is a solution for deploying a Kubernetes cluster locally on Linux. This is originally developed by Canonical(the publisher of Ubuntu). It uses [Snap](https://snapcraft.io/docs/getting-started) packages, an application packaging and isolation technology.

#### Prerequisites

A Linux distribution that supports Snap. Almost all Ubuntu releases support Snap out-of-box. At least 20G of disk space and 4G of memory are recommended

### MicroK8S commands

#### Install MicroK8s

```
sudo snap install microk8s --classic --channel=1.19
```

#### Join the group

```
sudo usermod -a -G microk8s $USER
sudo chown -f -R $USER ~/.kube
bash
```

#### Check the status

```
microk8s status --wait-ready
```

#### Access Kubernetes

Microk8s bundles it's own version of `kubectl`. To view nodes run

```
microk8s kubectl get nodes
```

It is easier to if alias is created and then we can run `kubectl` directly.

```
alias kubectl='microk8s kubectl'

root@chandi-dok1:~# kubectl get pods --all-namespaces
NAMESPACE     NAME                                      READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-847c8c99d-8vdt6   1/1     Running   0          4h36m
kube-system   calico-node-5mjbj                         1/1     Running   1          4h36m
default       nginx-6799fc88d8-ffrdj                    1/1     Running   0          4h28m
root@chandi-dok1:~#

```

#### Add-ons

MicroK8s uses the minimum of components for a pure, lightweight Kubernetes. You can view list of enabled `add-on`s issuing below command.

```
root@chandi-dok1:~# microk8s status
microk8s is running
high-availability: no
  datastore master nodes: 127.0.0.1:19001
  datastore standby nodes: none
addons:
  enabled:
    ha-cluster           # Configure high availability on the current node
  disabled:
    ambassador           # Ambassador API Gateway and Ingress
    cilium               # SDN, fast with full network policy
    dashboard            # The Kubernetes dashboard
    dns                  # CoreDNS
    fluentd              # Elasticsearch-Fluentd-Kibana logging and monitoring
    gpu                  # Automatic enablement of Nvidia CUDA
    helm                 # Helm 2 - the package manager for Kubernetes
    helm3                # Helm 3 - Kubernetes package manager
    host-access          # Allow Pods connecting to Host services smoothly
    ingress              # Ingress controller for external access
    istio                # Core Istio service mesh services
    jaeger               # Kubernetes Jaeger operator with its simple config
    knative              # The Knative framework on Kubernetes.
    kubeflow             # Kubeflow for easy ML deployments
    linkerd              # Linkerd is a service mesh for Kubernetes and other frameworks
    metallb              # Loadbalancer for your Kubernetes cluster
    metrics-server       # K8s Metrics Server for API access to service metrics
    multus               # Multus CNI enables attaching multiple network interfaces to pods
    prometheus           # Prometheus operator for monitoring and logging
    rbac                 # Role-Based Access Control for authorisation
    registry             # Private image registry exposed on localhost:32000
    storage              # Storage class; allocates storage from host directory
root@chandi-dok1:~#
```

Enable `add-on` using enable command. eg.

```
root@chandi-dok1:~# microk8s enable dns
Enabling DNS
Applying manifest
serviceaccount/coredns created
configmap/coredns created
deployment.apps/coredns created
service/kube-dns created
clusterrole.rbac.authorization.k8s.io/coredns created
clusterrolebinding.rbac.authorization.k8s.io/coredns created
Restarting kubelet
DNS is enabled

```

#### Starting and Stopping MicroK8s


```
microk8s stop
microk8s start
```



