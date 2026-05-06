# Module 06: Container Orchestration (Kubernetes)

## Why This Module

Running single containers is simple. Running hundreds across multiple machines with high availability, auto-scaling, and zero-downtime deployments requires orchestration. Diego's networking background (CCNA) and system administration skills directly apply to Kubernetes cluster management.

## Key Concepts

### Why Orchestration

- Single Docker host = single point of failure
- Manual container placement doesn't scale
- Service discovery, load balancing, self-healing need automation
- Diego's analogy: Like having a team of Linux admins automated — scheduling, monitoring, restarting services

### Kubernetes Architecture

**Control Plane**:
- `kube-apiserver`: The front door (REST API)
- `etcd`: Distributed key-value store (cluster state)
- `kube-scheduler`: Decides where pods run
- `kube-controller-manager`: Runs control loops (desired state → actual state)

**Worker Nodes**:
- `kubelet`: Node agent, ensures containers run as specified
- `kube-proxy`: Network proxy, manages service routing (Diego's networking applies here)
- Container runtime (containerd)

### Core Objects

- **Pod**: Smallest deployable unit (1+ containers sharing network/storage)
- **Deployment**: Manages pod replicas and rolling updates
- **Service**: Stable network endpoint for pods (ClusterIP, NodePort, LoadBalancer)
- **Ingress**: HTTP routing and TLS termination
- **ConfigMap/Secret**: Configuration injection
- **PersistentVolume/PVC**: Storage abstraction
- **Namespace**: Logical cluster partitioning

### Networking (Diego's CCNA applies)

- Pod-to-pod communication (flat network, no NAT)
- Service networking (kube-proxy, iptables/IPVS)
- DNS resolution (CoreDNS)
- Network policies (firewall rules for pods)
- Ingress controllers (nginx, traefik)
- Load balancing strategies

### Deployment Strategies

- Rolling updates (default)
- Blue/green deployments
- Canary deployments
- Rollbacks

### Operations

- Resource requests and limits
- Horizontal Pod Autoscaler (HPA)
- Liveness and readiness probes
- Pod disruption budgets
- Node affinity and taints/tolerations
- RBAC (Role-Based Access Control)

## Topics

1. Kubernetes architecture and components
2. kubectl CLI and resource management
3. Pods, Deployments, and ReplicaSets
4. Services and networking
5. Ingress and TLS
6. ConfigMaps, Secrets, and environment management
7. Persistent storage
8. RBAC and security
9. Helm charts (package management)
10. Kubernetes + Terraform (EKS/GKE provisioning)
11. GitOps with ArgoCD or Flux
