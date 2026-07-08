# 📘 Helm Introduction

Welcome to the **Helm Documentation**.

In this chapter, you'll learn what Helm is, why it was created, how it works, and why it has become the standard package manager for Kubernetes.

---

# 📑 Table of Contents

- What is Helm?
- Why do we need Helm?
- Problems without Helm
- Helm Architecture
- Helm Workflow
- Key Features
- Benefits of Helm
- Helm vs kubectl
- Key Terminologies
- Summary

---

# What is Helm?

Helm is the **package manager for Kubernetes**. It helps you package, deploy, upgrade, and manage Kubernetes applications using reusable templates called **Helm Charts**.

Instead of manually applying multiple Kubernetes YAML files, Helm allows you to deploy an entire application with a single command.

### Example

Without Helm:

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
kubectl apply -f ingress.yaml
```

With Helm:

```bash
helm install my-nginx .
```

---

# Why do we need Helm?

As Kubernetes applications grow, the number of YAML files also increases.

A typical application may require:

- Deployment
- Service
- ConfigMap
- Secret
- Ingress
- PersistentVolumeClaim (PVC)
- ServiceAccount
- Role & RoleBinding
- Horizontal Pod Autoscaler

Managing all these files manually becomes difficult.

Helm solves this problem by packaging everything into a single **Helm Chart**.

---

# Problems Without Helm

Without Helm, you may face:

- Duplicate YAML files
- Hardcoded values
- Difficult upgrades
- No rollback mechanism
- Environment-specific YAML duplication
- Time-consuming deployments
- Configuration management issues

Example:

If you have Dev, QA, UAT, and Production environments, you may end up maintaining four different sets of YAML files.

Helm allows you to use one chart with different configuration files for each environment.

---

# Helm Architecture

```
Developer
     │
     ▼
Helm CLI
     │
     ▼
Kubernetes API Server
     │
     ▼
Kubernetes Cluster
```

### Workflow

1. Developer creates or downloads a Helm Chart.
2. Helm reads the chart templates.
3. Values from `values.yaml` are injected into the templates.
4. Helm generates Kubernetes manifests.
5. These manifests are sent to the Kubernetes API Server.
6. Kubernetes creates the required resources.

---

# Helm Workflow

```
Create Helm Chart
        │
        ▼
Update values.yaml
        │
        ▼
Render Templates
        │
        ▼
Generate Kubernetes YAML
        │
        ▼
Deploy to Kubernetes
        │
        ▼
Upgrade / Rollback / Uninstall
```

---

# Key Features

- Reusable templates
- Parameterized deployments
- Version control
- Easy upgrades
- One-command installation
- Rollback support
- Dependency management
- Release history
- Environment-specific configuration

---

# Benefits of Helm

| Benefit | Description |
|----------|-------------|
| Reusability | One chart can be used multiple times |
| Simplicity | Deploy with a single command |
| Versioning | Manage chart versions easily |
| Rollback | Restore previous releases quickly |
| Automation | Integrates well with CI/CD pipelines |
| Consistency | Same deployment process across environments |

---

# Helm vs kubectl

| Feature | kubectl | Helm |
|----------|----------|------|
| Deploy Kubernetes resources | ✅ | ✅ |
| Package applications | ❌ | ✅ |
| Templating | ❌ | ✅ |
| Rollback support | ❌ | ✅ |
| Version management | ❌ | ✅ |
| Dependency management | ❌ | ✅ |
| Reusable deployments | ❌ | ✅ |

### When to use kubectl?

- Create or manage individual Kubernetes resources.
- Troubleshoot running workloads.
- Inspect cluster resources.

### When to use Helm?

- Deploy complete applications.
- Manage upgrades.
- Perform rollbacks.
- Reuse deployment templates.
- Deploy the same application across multiple environments.

---

# Key Terminologies

### Helm

The package manager for Kubernetes.

### Chart

A packaged Kubernetes application containing templates and configuration.

### Repository

A location where Helm Charts are stored and shared.

### Release

A running instance of a Helm Chart deployed to a Kubernetes cluster.

### values.yaml

Stores configurable values used by templates.

### Templates

Parameterized Kubernetes YAML files.

---

# Summary

In this chapter, you learned:

- What Helm is
- Why Helm is required
- Problems Helm solves
- Helm Architecture
- Helm Workflow
- Benefits of Helm
- Difference between Helm and kubectl
- Basic Helm terminology

In the next chapter, we'll learn how to install Helm and deploy our first Helm Chart.

---