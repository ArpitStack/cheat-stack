# Kubernetes Troubleshooting Guide

A practical guide for debugging common Kubernetes issues in production environments.

## Table of Contents

- [Pod Issues](#pod-issues)
- [Node Issues](#node-issues)
- [Networking Issues](#networking-issues)
- [Storage Issues](#storage-issues)
- [Cluster Issues](#cluster-issues)
- [Performance Issues](#performance-issues)
- [Security Issues](#security-issues)

## Pod Issues

Pod Stuck in Pending State:
```bash
# Check pod status and events
kubectl describe pod <pod-name>

# Check node resources
kubectl get nodes -o custom-columns=NAME:.metadata.name,ALLOCATABLE_CPU:.status.allocatable.cpu,ALLOCATABLE_MEMORY:.status.allocatable.memory

# Check if pods have resource requests that can't be fulfilled
kubectl get pod <pod-name> -o jsonpath='{.spec.containers[*].resources}'
```

Pod Stuck in ContainerCreating:
```bash
# Get detailed pod info
kubectl describe pod <pod-name>

# Check kubelet logs
kubectl logs -n kube-system kubelet-<node-name>

# Verify image existence and accessibility
kubectl get pod <pod-name> -o jsonpath='{.spec.containers[*].image}'
```

Pod in CrashLoopBackOff:
```bash
# Check pod logs
kubectl logs <pod-name>
kubectl logs <pod-name> --previous

# Check pod events
kubectl get events --field-selector involvedObject.name=<pod-name>

# Check container startup probe/liveness probe
kubectl get pod <pod-name> -o yaml | grep -A 10 livenessProbe
```

Pod in ImagePullBackOff:
```bash
# Check image details
kubectl describe pod <pod-name> | grep "Image:"

# Verify image pull secrets
kubectl get secrets | grep docker-registry
kubectl get secret <secret-name> -o yaml

# Check pod events
kubectl get events --field-selector involvedObject.name=<pod-name>
```

## Node Issues

Node NotReady State:
```bash
# Check node status
kubectl describe node <node-name>

# Check kubelet status
systemctl status kubelet

# Check kubelet logs
journalctl -u kubelet -n 100

# Verify node conditions
kubectl get node <node-name> -o jsonpath='{.status.conditions[*].type}'
```

Node Resource Exhaustion:
```bash
# Check node resource usage
kubectl top node <node-name>

# Get pods consuming most resources
kubectl top pods --containers

# Check resource quotas
kubectl get resourcequota
kubectl describe resourcequota <quota-name>
```

## Networking Issues

Service Connectivity Issues:
```bash
# Check service details
kubectl describe service <service-name>

# Verify endpoints
kubectl get endpoints <service-name>

# Test DNS resolution
kubectl run -it --rm debug --image=busybox -- nslookup <service-name>

# Check kube-proxy logs
kubectl logs -n kube-system kube-proxy-<pod-id>
```

Ingress Issues:
```bash
# Check ingress status
kubectl describe ingress <ingress-name>

# Verify ingress controller logs
kubectl logs -n ingress-nginx <ingress-controller-pod>

# Check ingress backend service
kubectl get svc <backend-service>
```

Network Policy Issues:
```bash
# List network policies
kubectl get networkpolicies

# Describe specific policy
kubectl describe networkpolicy <policy-name>

# Test network connectivity
kubectl run -it --rm debug --image=nicolaka/netshoot -- bash
```

## Storage Issues

PVC Stuck in Pending:
```bash
# Check PVC status
kubectl describe pvc <pvc-name>

# Verify storage class
kubectl get storageclass

# Check PV availability
kubectl get pv | grep Available
```

Volume Mount Issues:
```bash
# Check pod volume mounts
kubectl describe pod <pod-name> | grep -A 10 Volumes

# Verify PV binding
kubectl get pv | grep <pvc-name>

# Check kubelet volume logs
journalctl -u kubelet | grep volume
```

## Cluster Issues

Control Plane Problems:
```bash
# Check control plane pods
kubectl get pods -n kube-system

# Verify API server health
kubectl get --raw '/healthz?verbose'

# Check etcd status
kubectl -n kube-system exec -it etcd-<node-name> -- etcdctl endpoint health

# Check controller manager
kubectl -n kube-system logs kube-controller-manager-<node-name>
```

DNS Issues:
```bash
# Check CoreDNS pods
kubectl get pods -n kube-system -l k8s-app=kube-dns

# Verify DNS service
kubectl get svc -n kube-system kube-dns

# Test DNS resolution
kubectl run -it --rm debug --image=busybox -- nslookup kubernetes.default
```

## Performance Issues

High CPU/Memory Usage:
```bash
# Identify resource-heavy pods
kubectl top pods --all-namespaces --sort-by=cpu
kubectl top pods --all-namespaces --sort-by=memory

# Check container resource limits
kubectl get pods -o custom-columns=NAME:.metadata.name,CONTAINERS:.spec.containers[*].name,LIMITS:.spec.containers[*].resources.limits

# Monitor node metrics
kubectl top nodes --sort-by=cpu
```

Slow API Server Response:
```bash
# Check API server logs
kubectl logs -n kube-system kube-apiserver-<node-name>

# Monitor API server metrics
kubectl get --raw /metrics | grep apiserver_request

# Check etcd performance
kubectl -n kube-system exec etcd-<node-name> -- etcdctl endpoint status -w table
```

## Security Issues

RBAC Problems:
```bash
# Check user permissions
kubectl auth can-i --list --as=<username>

# Verify role bindings
kubectl get rolebindings,clusterrolebindings --all-namespaces

# Audit policy violations
kubectl logs -n kube-system kube-apiserver-<node-name> | grep audit
```

Pod Security Issues:
```bash
# Check pod security context
kubectl get pod <pod-name> -o jsonpath='{.spec.securityContext}'

# Verify pod service account
kubectl get pod <pod-name> -o jsonpath='{.spec.serviceAccountName}'

# Check container capabilities
kubectl get pod <pod-name> -o jsonpath='{.spec.containers[*].securityContext}'
```

## Pro Troubleshooting Tips

Create Debug Container:
```bash
# Attach debug container to running pod
kubectl debug <pod-name> -it --image=busybox --target=<container-name>

# Create standalone debug pod
kubectl run debug --rm -i --tty --image=nicolaka/netshoot -- bash
```

Log Analysis:
```bash
# Get recent pod logs with timestamp
kubectl logs <pod-name> --since=1h --timestamps

# Follow logs from multiple pods
kubectl logs -f -l app=<app-label> --all-containers

# Export logs to file
kubectl logs <pod-name> --tail=1000 > pod-logs.txt
```

Resource Monitoring:
```bash
# Watch pod resources in real-time
kubectl top pods --containers --watch

# Export metrics to Prometheus format
kubectl get --raw /metrics > metrics.txt
```