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