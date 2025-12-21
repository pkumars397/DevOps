# Kuber netes or K8s 

>container plus Orchestration 

## Containers 
>web server ,db ,messaging ,orchestration

>developers issues ,version issues of lib. dependencies ,have to continuously update.

>Matrix from hell ,new dev ,have to follow many instructions to installing dep.. 

>With docker run each services with seperate configurations etc.
>now dev just need to do ,make sure docker is installed on system.

@ Containers

>containers are completely isolated environments ,their own processes ,networking ,just like vm ,except they all share same os kernal.

i.e:
docker can run any os on top of it ,unless it is based on same kernal.

software1 software2 software3 software4 
--------- Docker ------------------
----------Os kernal----------------

## Virtual Machines                   vs Containers 


VM1 VM2 VM3 VM4                      C1 C2 C3 C4 .........
------Hypervisor--------------       ----------Docker---------
-------OS---------------------       ---------Os---------------
---Hardware Infrastructure----       ----------Docker-----------

>>each vm have their own os .        >> here not ,only app ,libs and dependencies.

>>complete isolation as diff os      >> less isolation

>>slow bootup                        >>fast bootup 


## Docker images and containers 

> images is package or template ,used to create one or more containers

>containers are running instance of images running in isolation.


### Conatiner Orchestration

  web container1         web container2
                                            >>> Docker Host
       mysql container 

>> lets say when load increases ,we have to scale .

----------------Orchestration----------------------
con1 con2 con3

>>automatically scale up or down ,based on load .

>>k8s is also orchestration techniq. (From Google)most popular with little difficult setup.

>>Docker Swarm,Mesos

## It is container orchestration techniq ,used to orchestrate hundreds of containers.


## K8s Nodes 
>>Nodes >> a machine physical or virtual .worker machine when containers will be launched.also known as minions in past.

>>Cluster >> set of nodes group together ,this way even if one node is fails ,Application still accessable .

>>Master >> monitoring of Clusters.Another node k8s installed on it.responsible for actual orchestration of node.

# when install K8s ...
>>API server ,etcd ,Scheduler ,kubelet ,Controller,Container Runtime.

>API server ...acts as frontend of k8s,CLI .
>etcd .. key value store to manage the cluster.implementing logs .
>Scheduler .. distrubing the work on across multiple nodes .
>Controller .. Brain behind orchestration,make decisions to bring new container if one down.
>container runtime .. use to run containers
>kubelet .. agent run on each node on the cluster.

# Master vs Worker Nodes..
>> Master node where containers are hosted. api server,etcd ,controller,scheduler .
>> Worker Node ... kubelet ,container runtime .

## Kubectl (Kube control)
>used to deploy or manage apps on kubernetes cluster,get cluster information etc.
 \\ kubectl run hello-minikube .. to deploy apps on cluster.
 \\kubectl cluster-info  .. gets cluster information.
 \\kubectl get nodes .. nodes info.