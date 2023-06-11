# Why we need container orchestrator

## Docker
- great for packaging and deploying containerized application
- limit with managing and scaling

## Container orchestrator
- scaling
- high availability
- load balancing
- resource management
- networking
- automated rollouts and rollbacks

## Architecture
| Control Plane (Master Node) |
| --------------------------- |
| API server (consider at the center) |
| etcd (top left) |
| scheduler ( bottom left ) |
| cloud controller manager (c-c-m) ( top right ) |
| controller manager ( bottom right )|

## etcd
- Distributed key value store
- Stores data about K8 objects
- needs to be aware of any changes
- we don't interect directly with etcd but via API server

## API server
- exposes K8 API
- authorizes requests
- is the main management components which help communicate with other components
- POC for all components in the control plane
- POC for 2 components in worker note (kubelet & kube-proxy)

## Controller manager
- compiles many controllers in a single binary (like node controller || replication controller & deployment controller)
- watches current state of each object thru API server
- fetches information from etcd & kubelet and compares with the desired state. If the states don't match, the associated controller manager will take action
- e.g., node controller watches the state of the nodes. If the kublet on node1 stops sending hearbeats to the API server, which is connected to the node controller, the node will fail.
- replication controller creates replicas of the pods if some pods are deleted

## Scheduler
- decides the worker node where the pod will be schedules on
- watches the API server for new pods
- it takes the decision based on multiple factors like worker node size,  resource req of containers, taints, tolerations, selectors, affinity etc..
- suppose you have a container which need 3 GB of RAM in 3 nodes ( 1 with 2 GB available, 2nd with 4 GB and 3rd with 6 GB ). It is obvious that the 1st node won't get the pod. 3rd will be selected as it has more resources (RAM)

## Cloud controller manager
- only if it is hosted in cloud
- it is a bridge between K8 API and cloud provider's API
- it is responsible for creating, upating, deleting resources in the cloud like VMs, loadbalancer, disks etc..

## Kubelet
- it is an agent that runs on each worker node
- connects to control plane's API server
- monitor health of worker nodes
- communicates with container runtime

## Container runtime
- is a software installed on every node
- ensures that nodes can run containers
- communicates with kubelet
- runs containers within pods
- `containerD` is the container runtime used in AKS

## Kube-proxy
- runs on each node
- is network proxy
- handles network traffic
- communicates directly with API server

## Worker node architecture
| worker node 1 |
|--------------|
|kubelet|
|kube-proxy|
|container runtime ( 1 pod ) |

| worker node 2 |
|--------------|
|kubelet|
|kube-proxy|
|container runtime ( 2 pod ) |

## What happens when a developer creates a pod
- suppose developer is using kubectl to reference a yaml file to create pods
- K8 API is based on `Go` language
- kubectl converts the yaml into json and sends to API server
- to do this, it uses a post request
- after API server receives the request to create the Pod, it validates the request and ensures that the user has the right permissions to create the Pods
- if the user is authorized, the API server upates the etcd database, which will store the config and states of the Pods
- next the schedular is notified with the details of the Pod
- the schedular finds a proper node to schedule the Pods
- scheduler updates the API server which updates the etcd
- API server contact the kubelet running on the chosen node
- kubelet infomrs the container runtime that it needs to run the Pods
- container runtime gives the state of the Pods to the kubelet
- kubelet continuously updates the API server which stores the state of the Pods in etcd
- if we had created a deployment, the cintroller manager would have come into picture
- contoller manager would have created a replication controller to ensure the desired states of the replicas of the Pods are held intact
- while creating deployment, a replicaset is created by the controller manager and the replicasets inturn creats and monitors the pods

## example
- lets say we created a deployment with 3 Pods - 1 on worker node 1 and 2,3 in worker node 2
- Pods hosts websites
- we want users to access the site
- one way is to create `service` type load-balancers
- service -> cloud controller manager -> cloud provider API and create a load-balancer resource in the public ip address associated with LB in cloud
- service distributes the traffic to Pods scheduled on both nodes
- public ip assigned to LB and internally the traffic is routed accordingly by the ip table rules configured by the kube-proxy
