ClusterIP Service (my-clusterip-service):

-Default service type.
-Internal-only service, accessible within the cluster.
-Exposes the service on a cluster-internal IP.

Headless Service (my-headless-service):

-ClusterIP set to None (clusterIP: None).
-Acts as a service discovery mechanism without a virtual IP.
-Used for stateful applications.

NodePort Service (my-nodeport-service):

-Exposes the service on each node's IP at a static port.
-Allows external access to the service.
-The nodePort field specifies the port on the nodes.

LoadBalancer Service (my-loadbalancer-service):

-Exposes the service externally using a cloud provider's load balancer.
-Allocates an external IP and automatically configures the load balancer.
