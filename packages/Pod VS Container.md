# POD VS CONTAINER

## POD Fundamentals
- Every Pod has a unique IP address
- Reachable by all other Pods in the cluster

## Pod abstraction of containers
- Lets say we have a postgres container (5234)
- On the server we can map the server port to the container port like 5000:5234
- We can also map another server port to cintainer port like 5002:5234
- But eventually if we have 100s for containers, we will run out of server ports and also we can't keep track of all the ports
- This is where Pod abstraction comes into picture
- Pod has its own ip and usually has one container
- Pod has its own namespace
- Pod has virtual ethernet connection
- Pod is a host like our laptop
- Pod has ip address and a range of port to allocate
- This means we don't have to worry about port mapping on the server where Pod is running
- This means on a server, we can have many pods/containers running on port 8080 and no conflicts because they run on self contained isolated machines
