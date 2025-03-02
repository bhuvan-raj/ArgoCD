# ArgoCD - GitOps Continuous Delivery for Kubernetes

## Overview
ArgoCD is a declarative, GitOps-based continuous delivery tool for Kubernetes applications. It ensures that the live state of a cluster matches the desired state defined in a Git repository.

## Features
- **Declarative GitOps deployment**
- **Automated synchronization** between Git and Kubernetes
- **Self-healing** mechanism to maintain desired state
- **Multi-cluster support** for managing multiple Kubernetes clusters
- **RBAC (Role-Based Access Control)** for secure access
- **Web UI, CLI, and API** for easy management

## Installation
### Prerequisites
- A running Kubernetes cluster
- `kubectl` CLI installed
- `argocd` CLI installed (optional but recommended)

### Install ArgoCD
```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Access ArgoCD UI
```sh
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Navigate to `https://localhost:8080` and log in using the initial admin password:
```sh
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

## Usage
### Login to ArgoCD CLI
```sh
argocd login localhost:8080
```

### Create an Application
```sh
argocd app create my-app \
  --repo https://github.com/example/repo.git \
  --path app-directory \
  --dest-server https://kubernetes.default.svc \
  --dest-namespace default
```

### Sync an Application
```sh
argocd app sync my-app
```

### Check Application Status
```sh
argocd app get my-app
```

## Configuration Options
ArgoCD supports various Kubernetes deployment methods:
- **Raw Kubernetes manifests**
- **Helm charts**
- **Kustomize configurations**
- **JSON/YAML patches**

## Security & RBAC
- ArgoCD supports **Role-Based Access Control (RBAC)** to manage user permissions.
- Authentication can be integrated with **SSO providers** (OAuth, LDAP, GitHub, etc.).

## Troubleshooting
### Check ArgoCD Logs
```sh
kubectl logs -n argocd deployment/argocd-server
```

### Restart ArgoCD Components
```sh
kubectl rollout restart deployment argocd-server -n argocd
```

## Resources
- [Official Documentation](https://argo-cd.readthedocs.io/)
- [GitHub Repository](https://github.com/argoproj/argo-cd)
- [CLI Reference](https://argo-cd.readthedocs.io/en/stable/user-guide/commands/)

## License
ArgoCD is licensed under the **Apache 2.0 License**.

---
Maintained by [Bhuvan Raj](https://github.com/bhuvan-raj)

