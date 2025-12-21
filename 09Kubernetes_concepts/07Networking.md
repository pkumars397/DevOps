# Basics of networking in k8s

>> Node ... POD ,192.168.1.2 ,single node k8s cluster
>> ip add. assigned to its POD.. 10.244.0.2 
(creates internal private network through internal ip)

# Cluster networking

> Node1 .. 192.168.1.2 , Node2 .. 192.168.1.3
(Cluster ip .. 10.244.0.0 ,pod1 10.244.0.2,pod2 10.244.0.2)
but doesn't work this way ,ip complexity

# conditions
> All containers/pods can communicate to one another without NAT
> All nodes can communicate with all containers 

> we don't have to set it up manually
