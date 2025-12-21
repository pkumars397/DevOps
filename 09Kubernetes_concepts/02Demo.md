## Total Pods

>> kubectl get pods

## Create new pod wiht Nginx image

>> kubectl run nginx-image=nginx

## what image is used to create new pod

>> kubectl describe pod podName

..look for container section and image used.

## Which nodes are these pods placed on

>>>kubectl get pods -o wide, will print some additional column

or >> kubectl describe pod podName

## How many containers are part of the pod webapp

>>> kubectl get pods webapp

OR

...under Ready column, denomonator is total number of container

>> kubectl describe pod podName

.. look under the containers section

## what images are used in webapp

>>>same, look for image name in containers.

## imagePullBackof >> image not available on dockerhub.

## what Ready column indicate in output of get command

>> total running containers in pod/total number of containers in pod

## delete webapp pod

>> kubectl delete pod webapp

## create a new pod "redis" with image redis123

..two ways via command or yaml file

>>> cat > redis-pod.yaml (copy paste the def from k8s site)

>>> kubectl create -f redis-pod.yaml

## fix the image on pod to "redis"

..two way

>> kubectl edit pod redis

(will go into the vi editor edit the image)

OR

>>vi redis-pod.yml

(update)

>>kubectl create -f redis-pod.yaml