# Kubernetes (kubectl) Commands Cheatsheet

A comprehensive guide for kubectl commands used in production environments.

## Table of Contents

- [Cluster Management](#cluster-management)
- [Pod Operations](#pod-operations)
- [Deployment Operations](#deployment-operations)
- [Service & Networking](#service--networking)
- [Configuration & Security](#configuration--security)
- [Monitoring & Logging](#monitoring--logging)

## Cluster Management

Get cluster information:
```bash
# Display cluster info
kubectl cluster-info

# Get all nodes with details
kubectl get nodes -o wide

# Check component status
kubectl get componentstatuses
```

## Pod Operations

Basic pod commands:
```bash
# List all pods
kubectl get pods
kubectl get pods -o wide
kubectl get pods --all-namespaces

# Get pod details
kubectl describe pod <pod-name>

# Create pod from file
kubectl create -f pod.yaml

# Delete pod
kubectl delete pod <pod-name>
kubectl delete pod <pod-name> --grace-period=0 --force

# Execute command in pod
kubectl exec -it <pod-name> -- /bin/bash
```

## Deployment Operations

Manage deployments:
```bash
# Create/Update deployment
kubectl apply -f deployment.yaml

# List deployments
kubectl get deployments

# Update image
kubectl set image deployment/<deployment-name> <container-name>=<new-image>

# Scale deployment
kubectl scale deployment <deployment-name> --replicas=3

# Rollout status
kubectl rollout status deployment/<deployment-name>

# Rollout history
kubectl rollout history deployment/<deployment-name>

# Rollback deployment
kubectl rollout undo deployment/<deployment-name>
kubectl rollout undo deployment/<deployment-name> --to-revision=2
```

## Service & Networking

Service management:
```bash
# List services
kubectl get services

# Create service
kubectl create service clusterip <service-name> --tcp=80:80

# Expose deployment as service
kubectl expose deployment <deployment-name> --port=80 --target-port=8080

# Port forward
kubectl port-forward service/<service-name> 8080:80
```

Network debugging:
```bash
# Test service DNS
kubectl run -it --rm debug --image=busybox -- nslookup kubernetes.default

# Check service endpoints
kubectl get endpoints <service-name>
```

## Configuration & Security

ConfigMaps and Secrets:
```bash
# Create ConfigMap
kubectl create configmap <config-name> --from-file=<path/to/file>
kubectl create configmap <config-name> --from-literal=key1=value1

# Create Secret
kubectl create secret generic <secret-name> --from-literal=key1=value1
kubectl create secret generic <secret-name> --from-file=<path/to/file>

# Get ConfigMap/Secret
kubectl get configmap <config-name> -o yaml
kubectl get secret <secret-name> -o yaml
```

RBAC:
```bash
# Create role
kubectl create role pod-reader --verb=get,list,watch --resource=pods

# Create role binding
kubectl create rolebinding read-pods --role=pod-reader --user=jane

# Check permissions
kubectl auth can-i --list
```

## Monitoring & Logging

Resource monitoring:

```bash
# Get resource usage
kubectl top nodes
kubectl top pods

# Get metrics
kubectl get --raw "/apis/metrics.k8s.io/v1beta1/nodes"
```

Events and logs:

```bash
# Get cluster events
kubectl get events --sort-by='.metadata.creationTimestamp'

# Get specific resource events
kubectl get events --field-selector involvedObject.name=<resource-name>
```

## Pro Tips

Working with labels:

```bash
# Get pods with labels 
kubectl get pods --show-labels

# Select by label
kubectl get pods -l environment=production,tier=frontend

# Add/Update label
kubectl label pods <pod-name> environment=production

# Remove label
kubectl label pods <pod-name> environment-
```

Output formatting:

```bash
# Custom columns
kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase

# JSON path
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'

# Sort output
kubectl get pods --sort-by=.metadata.creationTimestamp
```



