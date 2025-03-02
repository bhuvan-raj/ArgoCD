# Sample ArgoCD Application

## Overview
This repository contains an ArgoCD application manifest that deploys a sample application to a Kubernetes cluster using GitOps principles.

## Prerequisites
- A running **Kubernetes cluster**
- **kubectl** installed
- **ArgoCD installed** in your cluster
- **ArgoCD CLI (optional but recommended)**

## Deployment Steps

### 1. Modify the Application Manifest
Before applying the ArgoCD application manifest, update the `application.yaml` file:
- Change the **source** (`repoURL` and `path`) to match your Git repository.
- Change the **destination** (`server` and `namespace`) to match your Kubernetes cluster.

### 2. Apply the ArgoCD Application Manifest
To create the application in ArgoCD, run:
```sh
kubectl apply -f application.yaml -n argocd
```

### 3. Check Application Status
Verify that ArgoCD has registered the application:
```sh
argocd app list
argocd app get sample-app
```

### 4. Sync the Application
To deploy the application from Git, run:
```sh
argocd app sync sample-app
```

### 5. Enable Auto-Sync (Optional)
To keep the application automatically updated with changes from Git:
```sh
argocd app set sample-app --sync-policy automated
```

## What Happens After Applying This?
- ArgoCD continuously monitors the Git repository.
- If any changes occur, it **updates the Kubernetes cluster** automatically.
- This ensures that **Git is the single source of truth** (GitOps model).

## Cleanup
To remove the application from ArgoCD:
```sh
argocd app delete sample-app
```

To uninstall ArgoCD:
```sh
kubectl delete namespace argocd
```

## Resources
- [ArgoCD Official Documentation](https://argo-cd.readthedocs.io/)
- [ArgoCD GitHub Repository](https://github.com/argoproj/argo-cd)

---
Maintained by [Bhuvan Raj](https://github.com/bhuvan-raj)

