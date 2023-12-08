Certainly! Here are the commands related to the mentioned topics:

### **Minikube Installation:**
```bash
# Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start Minikube cluster
minikube start

# Check Minikube status
minikube status

# Stop Minikube
minikube stop
```

### **kubectl:**
```bash
# Display Kubernetes version
kubectl version

# Display cluster information
kubectl cluster-info

# List all nodes
kubectl get nodes
```

### **Pods:**
```bash
# List all pods
kubectl get pods

# Describe a pod
kubectl describe pod [pod-name]

# Get pod logs
kubectl logs [pod-name]
```

### **Replica Sets:**
```bash
# List replica sets
kubectl get replicasets
```

### **Deployments & StatefulSets:**
```bash
# List deployments
kubectl get deployments

# Scale a deployment
kubectl scale deployment [deployment-name] --replicas=[number]
```

### **ConfigMap & Secret:**
```bash
# List config maps
kubectl get configmaps

# List secrets
kubectl get secrets
```

### **Debugging Commands:**
```bash
# Open a shell inside a running pod
kubectl exec -it [pod-name] -- /bin/bash
```

### **Delete Pods:**
```bash
# Delete a pod
kubectl delete pod [pod-name]
```

### **Namespaces:**
```bash
# List namespaces
kubectl get namespaces

# Create a namespace
kubectl create namespace [namespace-name]
```

### **YAML File Demos:**
```bash
# Apply YAML files
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
kubectl apply -f persistentvolumeclaim.yaml
kubectl apply -f storageclass.yaml
```

Remember to replace placeholders such as `[pod-name]`, `[deployment-name]`, `[namespace-name]`, etc., 
with your actual resource names. Also, ensure that your Minikube cluster is running before executing these commands.
