## going to install basic k8s cluster using minikube

>> first install kubectl on system. CLI to work with k8s cluster.
steps 
1. download binary 
2. make it executable
3. move to /usr/local/bin/kubectl

or using other way snap, >> sudo snap install kubectl --classic 

>>kubectl version --client

# now install minikube 
1. virtualization should be enable on laptop.
>> command ,->> grep -E --color 'vmx|svm' /proc/cpuinfo

>>verify kubectl
>>install a Hypervisor
(virtualBox)

>>follow instruction on k8s page to install minikube

>>minikube start --driver=virtualbox 

>> minikube status, check minikube is installed or not.

## commands 
>>kubectl get nodes , minikube  will come
>>kubectl create deployment hello-minikube --image=k8s.gcr.io/ecoserver:1.10

>>kubectl get deployments

