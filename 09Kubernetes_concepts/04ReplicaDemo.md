## Demo Replicas

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: myapp-replicaset
  labels:
   app:myapp
spec:
  selector:
   matchLabels:
     app: myapp 
  replicas: 3
  template:
    (copy from metadata of pod)
    metadata:
      name: nginx-2
      labels:
        app: myapp (same as matchLabels)
    spec:
      containers:
        - name: nginx
          image: nginx
        
>> kubectl create -f replicaset.yml
>> kubectl get replicaset

>> kubectl get pods 
(three pods for replicaset created)
myapp-replicaset-jkfj
myapp-replicaset-ldkf
myapp-replicaset-siak

# lets see what happens when we delete one of these pods

>> kubectl delete pod myapp-replicaset-jkfj
(this pod of replicaset will be deleted)

>> kubectl get pods 
myapp-replicaset-newPodCreated ... automatically created
myapp-replicaset-ldkf
myapp-replicaset-siak


>> kubectl describe replicaset myapp-replicaset

(all details of replicaset)

... will show which pods how much life and all 

>> replicaset insures minmum number of replicas(pods) are available

# new pod using same label which replicaset uses (matachLabels: app:myapp)

apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp (same label of replicaset)
    type: front-end

spec:
   containers: (list)
    - name: nginx-container  .> dictionary.
      image:nginx

>> kubectl create -f podDefinition.yaml

>> kubectl get pods
(replicaset will terminate the creation of pod with same label)

## update the replicaset (trying to scale up the application)
# first method
>> kubectl edit replicaset myapp-replicaset
(open editor(vim))

.. update the replicas and save exit(i.e 4)

>> kubectl get pods 
(now 4 pods)

# second method
>> kubectl scale replicaset myapp-replicaset --replicas=2
>> kubectl get pods
(will scale down)

-----------------Test-------------

# How many pods >> kubectl get pods

# How many replicaset >> kubectl get rs

# How many pods desired in our rs >> desire column

# what image used to create pods in our rs

>> kubectl describe replicaset , image key

# How many pods are ready in our rs 
>> kubectl get replicasets , look for ready column

# Why pods are not ready yet 
>> Status ImagePullBackoff 
>> kubectl describe pod podNamers
(failed to pull ,image doesn't exist)

# Delete one pod,but rs will auto scale up ,will create a new pod.

(Replicaset ensures that desired pods always available)

# Create a rs using yaml file
>> kubectl create -f replicaset-definition.yaml
(version issue,apps/v1)

.. selector doesn't match template labels
>> template label should be used in matchLabels.

(first create a pod using template definition,so labels should be same)

# delete replicaset >> kubectl delete rs replica-1 replica-2

# Fix replicaset to use correct image 

>> kubectl edit rs replica-1
(opens vi editor)
(but still not create fresh rs,still uses old image)
... reason ,doesn't carry forward the changes to new rs.

> so delete all pods or delete rs ,then create .

>> before deleting rs , export the definition file.

>> kubectl get rs new-rs -o yaml
(shows definition)

.. save 
>> kubectl get rs new-rs -o yaml > new-replica-set.yaml
..now delete
>> kubectl delete rs new-rs

>> kubectl create -f new-replica-set.yaml

# scale to 5 pods
>> kubectl scale rs new-replica --replicas=5 

Or

>> kubectl edit rs new-replica.
(this time it will auto scale)