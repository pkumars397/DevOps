# Services
>> enables communicate between pods(frontend pods or backend pods)

>> cummunicate with ip of node and laptop ip using service called NodePort service

>> ClusterIp .. virtual ip

>>LoadBalancer .. types of service

-------NodePort service ------------
>> mapping port on node and port on pod
   port30008 on node....service...port 80... port 80 on pod

# How to create a service 
??service-definition.yaml

apiVersion:v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: NodePort
  ports:
   - targetPort: 80 (if not provided,takes port)
     port: 80
     nodePort: 30008 (if not mentioned,free port used)
  selector:
    app: myapp
    type: front-end

>> kubectl create -f service-definition.yaml

>> kubectl get services

>> curl http://192.168.1.2:30008 , to access web service or web browser

if multiple pods on node,then it matches with same label of all pods

so same service for all pods ,with different ip of pod.(automatically)

>> minikube service myapp-service --url ,show url on which u can access the app

## ClusterIp
> few pods for frontend
> few pods for backend
> few for redis

> right way to establish connection between these
> pods can go down ,so can't rely on ip address
> k8s service can help us to group these.

??service-definition.yaml
apiVersion:v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: clusterIP
  ports:
   - targetPort: 80 (if not provided,takes port)
     port: 80
  selector:
    app: myapp
    type: back-end

>> kubectl create ...
>> kubectl get services


## LoadBalancer

voting app pods  ............ result-app

192.168.56.70:30035             192.168.56.70:31061

but want url ..
example-voting.com              example-result.com

                       ..
                       LoadBalancer (only works with cloud platform)

apiVersion:v1
kind: Service
metadata:
  name: myapp-service
spec:
  type: LoadBalancer
  ports:
   - targetPort: 80 (if not provided,takes port)
     port: 80
     nodePort:30008
  selector:
    app: myapp
    type: front-end

>> default service is ClusterIp which kubernetes automatically creates .