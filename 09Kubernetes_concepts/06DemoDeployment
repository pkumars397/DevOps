# Demo
>> kubectl create -f Deployment-definition.yaml

>> kubectl rollout status deployment.apps/myapp-deployment 

>> kubectl delete deployment myapp-deployment
(delete deployment)

>> kubectl create -f deployment.yaml

>> kubectl rollout status deployment.apps/myapp-deployment
(will follow rollingback method one at a time)

>> kubectl rollout history deployment.apps/myapp-deployment 
 
----
>> kubectl delete deployment myapp-deployment 

>> kubectl get pods 
(wait for all to go away)

(create again deployment again)
>> kubectl create -f deployment.yaml --record 

>> kubectl rollout status deployment.apps/myapp-deployment

>> kubectl rollout history deployment.apps/myapp-deployment
(now it will record the command)


>>kubectl describe deployment myapp-deployment 

---change image--

>> kubectl edit deployment myapp-deployment --record 
(set diff image,nging:1.18 )

>> kubectl rollout status deployment.apps/myapp-deployment


>> kubectl describe deployment myapp-deployment

---another way---
>> kubectl set image deployment myapp-deployment nginx=nginx:1.18-perl --record 
(changes will be recorded in rollout history )

(now history will track all the changes to deployment)

----revert back---

>> kubectl rollout undo deployment/myapp-deployment

>> status command(all status)

>> kubectl describe deployment myapp-deployment
(will show previous image)

--- more faulty changes --
>> kubectl edit deployment myapp-deployment 

>> kubectl rollout status deployment.apps/myapp-deployment
(will stuck because wrong image)

>> kubectl get pods 

(but application will not affacted because ,new pods are not created so it doesn't deleted old ones)... app will be up

