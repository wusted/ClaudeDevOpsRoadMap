# Module 06: Container Orchestration — Hands-On Exercises

## Module Repository: `kubernetes-platform`

All deliverables for this module live in `repos/kubernetes-platform/` and on GitHub at `github.com/<username>/kubernetes-platform`. Create it with `/setup-repo` before starting Exercise 6.1.

The repo's README should describe it as a portfolio of Kubernetes manifests, Helm charts, EKS provisioning code, and ArgoCD GitOps configurations — a complete platform-engineering project.

Replace earlier paths like `devops-lab/kubernetes/...` with in-repo equivalents (e.g., `app/`, `charts/myapp/`, `eks/`, `gitops/`).

---

## Exercise 6.1: Local Kubernetes Cluster

**Objective**: Set up a local Kubernetes environment and deploy your first application.

**Steps**:
1. Install and start minikube or kind (Kubernetes in Docker)
2. Verify cluster: `kubectl cluster-info`, `kubectl get nodes`
3. Deploy nginx: `kubectl create deployment nginx --image=nginx`
4. Expose it: `kubectl expose deployment nginx --port=80 --type=NodePort`
5. Access the service and verify
6. Scale: `kubectl scale deployment nginx --replicas=3`
7. Kill a pod and watch Kubernetes recreate it
8. Explore: `kubectl get pods -o wide`, `kubectl describe pod <name>`, `kubectl logs <name>`

**Validation**: 3 replicas running, self-healing works (killed pod replaced), service accessible

---

## Exercise 6.2: Declarative Manifests and Deployments

**Objective**: Manage Kubernetes resources with YAML manifests (infrastructure as code pattern).

**Steps**:
1. Create `devops-lab/kubernetes/app/` with:
   - `namespace.yaml`
   - `deployment.yaml` (your Docker image from Module 05)
   - `service.yaml`
   - `configmap.yaml` (application configuration)
   - `secret.yaml` (database credentials, encoded)
2. Apply all: `kubectl apply -f devops-lab/kubernetes/app/`
3. Configure resource requests and limits
4. Add liveness and readiness probes
5. Perform a rolling update (change image tag)
6. Rollback: `kubectl rollout undo deployment/<name>`
7. Check rollout history: `kubectl rollout history deployment/<name>`

**Validation**: All resources in namespace, rolling update works, rollback restores previous version

---

## Exercise 6.3: Networking and Ingress

**Objective**: Configure service discovery, DNS, and HTTP routing.

**Context**: Diego's CCNA background applies directly here — pod networking, service routing, DNS.

**Steps**:
1. Deploy two services (frontend + backend) in the same namespace
2. Verify pod-to-pod DNS resolution: `kubectl exec <frontend-pod> -- nslookup <backend-service>`
3. Install an ingress controller (nginx-ingress on minikube)
4. Create an Ingress resource routing:
   - `/api/*` → backend service
   - `/` → frontend service
5. Add TLS with a self-signed certificate
6. Create a NetworkPolicy that:
   - Allows frontend → backend traffic
   - Denies all other inter-pod traffic
7. Test the NetworkPolicy (attempt blocked connections)

**Validation**: DNS works, ingress routes correctly, TLS terminates, NetworkPolicy blocks unauthorized traffic

---

## Exercise 6.4: Helm Charts

**Objective**: Package the application as a reusable Helm chart.

**Steps**:
1. Create a Helm chart: `helm create devops-lab/kubernetes/charts/myapp`
2. Template the deployment with values for:
   - Image repository and tag
   - Replica count
   - Resource limits
   - Environment variables
3. Create `values-dev.yaml` and `values-prod.yaml` with different configurations
4. Install: `helm install myapp ./charts/myapp -f values-dev.yaml`
5. Upgrade with new values: `helm upgrade myapp ./charts/myapp -f values-prod.yaml`
6. Rollback: `helm rollback myapp 1`
7. Package and consider publishing to a chart repository

**Validation**: Chart installs cleanly, values override works, upgrade and rollback function correctly

---

## Exercise 6.5: Kubernetes with Terraform (EKS)

**Objective**: Provision a managed Kubernetes cluster using Terraform.

**Prerequisites**: AWS account (this will incur costs — use free-tier where possible and destroy promptly)

**Steps**:
1. Create `devops-lab/terraform/eks/`
2. Use Terraform to provision:
   - VPC with public/private subnets
   - EKS cluster
   - Node group (2x t3.small)
3. Configure kubectl to connect: `aws eks update-kubeconfig`
4. Deploy your Helm chart to the EKS cluster
5. Create a GitHub Actions workflow that deploys to EKS on merge
6. **IMPORTANT**: Destroy everything when done (`terraform destroy`)

**Validation**: EKS cluster running, app deployed via Helm, accessible via LoadBalancer, CI deploys work

---

## Exercise 6.6: GitOps with ArgoCD

**Objective**: Implement GitOps — deploy by pushing to git, not running kubectl.

**Steps**:
1. Install ArgoCD on your cluster
2. Create a GitOps repository with Kubernetes manifests
3. Configure ArgoCD to watch the repository
4. Make a change (update image tag) via PR
5. Observe ArgoCD detect and apply the change
6. Intentionally drift (manual kubectl edit) and watch ArgoCD correct it
7. Set up sync policies: auto-sync, prune, self-heal

**Validation**: Changes deployed via git commits only, drift auto-corrected, no manual kubectl needed
