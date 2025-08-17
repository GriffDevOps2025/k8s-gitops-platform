# Deployment Guide - Enterprise GitOps Platform

> **Complete step-by-step guide for deploying the enterprise GitOps platform from scratch**

## 📋 Prerequisites

### **System Requirements**
- **Operating System**: Windows 10/11, macOS, or Linux
- **Memory**: Minimum 8GB RAM (16GB recommended)
- **Storage**: 20GB free disk space
- **Network**: Internet connection for container image downloads

### **Required Software**
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) with Kubernetes enabled
- [kubectl](https://kubernetes.io/docs/tasks/tools/) CLI tool
- [Git](https://git-scm.com/downloads) for repository management
- Text editor (VS Code recommended)

### **Verification Commands**
```bash
# Verify Docker is running
docker --version
docker ps

# Verify Kubernetes is enabled
kubectl cluster-info

# Verify Git is available
git --version
```

## 🚀 Quick Start (5 Minutes)

### **1. Clone Repository**
```bash
git clone https://github.com/GriffDevOps2025/k8s-gitops-platform.git
cd k8s-gitops-platform
```

### **2. Install ArgoCD**
```bash
# Create ArgoCD namespace
kubectl create namespace argocd

# Deploy ArgoCD
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Wait for ArgoCD to be ready (2-3 minutes)
kubectl wait --for=condition=available --timeout=300s deployment/argocd-server -n argocd
```

### **3. Deploy GitOps Applications**
```bash
# Deploy all platform applications
kubectl apply -f infrastructure/argocd/applications/

# Verify applications are created
kubectl get applications -n argocd
```

### **4. Set up Local DNS**
Add these entries to your hosts file:

**Windows**: