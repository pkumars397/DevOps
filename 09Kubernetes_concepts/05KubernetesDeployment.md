## How to deploy k8s app in prod. envir.

>> Each container are encapsulated into a pod
>> then comes deployment ,using rolling updates ,undo changes etc.

>> Deployment Definition file. Similar to Pods ,except kind: Deployment

>> kubectl create -f deployment-definition.yml

>> kubectl get deployments

>> kubectl get replicaset

>> kubectl get pods

# commands 
>> kubect get all ,everything deployment ,replicaset followed by pods.

--------------------------------------------------------------------------------

# Demo
??deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-deployment
  labels:
    tier: frontend
    app: nginx
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

>>kubectl create -f deployment.yaml
>>kubectl describe deployment myapp-deployment

-------------------------------------------------------------
# Rollout and versioning
>> when u first trigger a deployment it triggers a rollout .. rivision 1

>> when app upgraded ,new rollout trigger ... rivision 2

>> this helps to rollback to previous deployment.


>> kubectl rollout status deployment/myapp-deployment

>>kubectl history rollout deployment/myapp-deployment


# dep. stratgy
>> destroy all instances ,then deploy again ... problem application down .. Recreate stratgy ,not default

>> default one , take down older version and bring back newer one one-by-one ... if not specified stratgy ,this one used


## updating the deployment

>> updating replicas,images etc.

>> kubectl apply -f deployment-definition.yaml

OR 

>> kubectl set image deployment/myapp-deployment  \nginx=nginx:1.9.1
.. most be careful ,when using this.

# Diff recreate and rollingupdate

>> recreate .. old rs will be scaledown to zero and then new rs will be create.

>>rollingupdate .. scale down one by one then create new one.

>> kubectl get rs .. will show details ,in rollingupdate

## rollback update

>> kubectl rollout undo deployment/myapp-deployment 
.. will bring back the old rs 

>> for check , kubectl get rs before and after this rollout j

## kubectl run nginx --image=nginx .. direct pod , its deployment only ,not using definition file . automatically created rs ,pods all ..


----------------Revision-------------------------------
# Create 
>> kubectl create -f deployment-defintion.yaml

# Get
>> kubectl get deployments

# Update
>> kubectl apply -f deployment-definition

>> kubectl set image deployment/myapp-deployment nginx=nginx:1.9.1 

# Status 
>> kubectl rollout status deployment/myapp-deployment

>> kubectl rollout history deployment/myapp-deployment

>> kubectl rollout undo deployment/myapp-deployment 