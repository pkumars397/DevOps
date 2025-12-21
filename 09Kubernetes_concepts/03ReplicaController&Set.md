## Replica Controllers and replicaset

## controlers are brain behind käs

# Replica controller
>> helps us to run multiple instance of kas pods.

>> bring up new pod when a pod fails.

>> Load Balancing and scaling, when number of users increases we can deploy additional pods on different nodes.

## replication controller is old, replica set is new way

>>we will use replica set only.

# replication controller

?? rc-definition.yml

apiVersion: v1
kind: ReplicationController
metadata:
  name: myapp-rc
  labels:
    app: myapp
    type: front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app:myapp
        type: front-end
    spec:
      containers:
       - name: nginx-contatiner
         image: nginx

  replicas: 3

>>kubectl create -f rc-definition.yml

>>>kubectl get replicationcontroller

>>kubectl get pods

(the pods which are being created by the rcontroller)

# replica set

??replicaset-definition.yml

apiVersion: apps/v1
kind: Replicaset
metadata:
  name: myapp-replicaset
  labels:
    app:myapp
    type:front-end
spec:
  template:
    metadata:
      name: myapp-pod
      labels:
        app:myapp
        type:front-end
    spec:
      containers:
       - name: nginx-contatiner
        image: nginx
  replicas: 3
  selector: (required)
      matchLabels:
      type: front-end

>>>kubectl create -f replicaset-definition.yml

>>kubectl get replicaset

>>kubectl get pods


------------------------------
# Labels and Selectors

>>monitor the pods if any one fails deploy new one.

>>inside selector >>> matchlabels >>type : same as pod type

# Scale

>>update in definition file

>>kubectl replace -f replicaset-definition.yml

OR

>>kubectl scale replicas-6-f replicaset-definition.yml

OR 
>> kubectl scale-replicas-6 replicaset myapp-replicaset (type and name of type, 1.e replicaset here)

Commands Revise

>>>kubectl create -f replicaset-definition.yml

>>kubectl get replicaset

>>>kubectl delete replicaset myapp-replicaset (Also deletes all underlying pods)

>>kubectl replace -f replicaset-definition.ymlI

(kubectl scale--replicas=6 replicaset-definition.yml)