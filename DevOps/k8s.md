Pod:
* Smallest unit of k8s
* abstraction over container
* 1 app per pod
* every pod get its IP addr (**this IP changes when pod restart**)

Service:
* permanent IP addr
* bind to pods
* External service : type of service expose to outside
Ingress:
* like domain binds to service

ConfigMap:
* external configuration of app
* ex : Bind DB_URL
* **don't put credential in configmap **
Secret:
* like ConfigMap, but uses for sensetive data (credential)

Volumes:
* attach storage to pods
* can be local or remote
* k8s its sell doesnt manage data persitance 

Depolyment:
* blueprint for pods
* determine how many replicate pod you want
* **can't replicated database ** : statefulSet for stateFUL app or database
* DB often hosted ouside k8s cluster by statefulSet is hard to configure

![](https://i.imgur.com/4bxAFcQ.png)


## k8s architecture
 
 worker machine
 * each Node has multiple pods
 * worker nodes do actual work

![](https://i.imgur.com/pRoSYui.png)

Workder machine should have:
* **Kubelet** interacts with both container and node
* container runtime
* Kube proxy

interact with cluster: master node
* Api server : cluster gateway
* Scheduler :  
* Contorller manager
* etcd : cluster brain, store cluster changes in key value store 

## minikube

Test/Local cluster Setup
* create virtual box
* Node runs in Virtual box
* 1 node k8s cluster

## kubectl
interact with cluster (CLI)
command line tool for k8s cluster


## Install on arch

**注意： Virtualbox中沒辦法使用KVM，只能在virtualbox中用virtualbox**

### KVM的安裝
```bash
sudo pacman -Sy libvirt qemu ebtables dnsmasq
```

```bash
sudo usermod -a -G libvirt $(whoami)  
newgrp libvirt
```
```bash
sudo systemctl start libvirtd.service  
sudo systemctl enable libvirtd.service  
   
sudo systemctl start virtlogd.service  
sudo systemctl enable virtlogd.service
```

### Virtualbox內請安裝virtualbox

docker:
```bash
sudo pacman -Sy docker-machine
```
```bash
yaourt -Sy docker-machine-driver-kvm2
```

minikube:
```bash
pacman -S minikube kubectl
```

Start minikube:
```bash
minikube start --driver=virtualbox
```