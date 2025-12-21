> lets assume app already developed ,and build into docker images.
> also cluster seted up.

# POD ,single instance of an app,smallest object you can create in k8s.

>> if number of user increase ,we have to increase instances i.e POD. which will run on same node.

>> can also add new nodes.

>> multiple container PODs 

>> can also create helper container for same POD.when pod destroyed .that container also .

## PODs again

>> docker run python-app ,one container intially 
>> docker run python-app ,second container
>> docker run python-app ,third container

>> docker run helper -link app1 
>> docker run helper -link app2 
>> docker run helper -link app3 

>in pod ,k8s does all of these automatically ,just define what container a pod consist of.

> multi pod container rare. mainly we will use single pod.

## kubectl commands
>>kubetcl run nginx --image nginx ,pod created 

>>kubectl get pods ,will show pods available


## pod is most basic unit in kubernetes.

..> kubectl run nginx --image=nginx ,pod name can be anything,but image name should be image of docker hub,or docker registry image.

>>kubectl get pods , to get pod which is running and all

>>kubectl decribe pod nginx, information about pod in detail.

>>kubectl get pods -o wide , also more info about pod.