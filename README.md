# Helm_chart
# 🚀 Helm Chart Complete Guide

> A complete Helm Chart reference for Kubernetes beginners to advanced users.
> This repository contains Helm concepts, commands, chart structure, templating, best practices, and real-world examples.

---

# Table of Contents

1. What is Helm?
2. Why Helm?
3. Helm Architecture
4. Install Helm
5. Helm Commands
6. Helm Chart Structure
7. Chart.yaml
8. Values.yaml
9. Templates
10. Template Functions
11. Built-in Objects
12. Helpers (_helpers.tpl)
13. Variables
14. Conditional Statements
15. Loops
16. Pipelines
17. Default Values
18. Named Templates
19. Include vs Template
20. Files Directory
21. ConfigMap
22. Secret
23. Deployment
24. Service
25. Ingress
26. Hooks
27. Lifecycle
28. Dependencies
29. Helm Repository
30. Packaging Charts
31. Versioning
32. Helm Upgrade
33. Rollback
34. Uninstall
35. Debugging
36. Linting
37. Best Practices
38. Interview Questions

---

# 1. What is Helm?

Helm is the package manager for Kubernetes.

Just like:

- apt → Ubuntu
- yum → RHEL
- npm → NodeJS

Helm manages Kubernetes applications using reusable templates called **Charts**.

Without Helm:

```
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml
kubectl apply -f configmap.yaml
kubectl apply -f secret.yaml
```

With Helm:

```
helm install myapp .
```

---

# 2. Why Helm?

Benefits

- Reusable templates
- Easy upgrades
- Easy rollback
- Environment-specific configuration
- Parameterized deployments
- Less YAML duplication
- Version control
- Dependency management

---

# 3. Helm Architecture

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

---

# 4. Install Helm

Linux

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

Windows

```
choco install kubernetes-helm
```

Verify

```
helm version
```

---

# 5. Common Helm Commands

Create chart

```
helm create mychart
```

Install

```
helm install nginx ./mychart
```

Upgrade

```
helm upgrade nginx ./mychart
```

Rollback

```
helm rollback nginx 1
```

Delete

```
helm uninstall nginx
```

List releases

```
helm list
```

History

```
helm history nginx
```

Lint

```
helm lint .
```

Template

```
helm template .
```

Dry Run

```
helm install demo . --dry-run
```

Debug

```
helm install demo . --debug
```

---

# 6. Helm Chart Structure

```
mychart/

│

├── Chart.yaml

├── values.yaml

├── charts/

├── templates/

│     deployment.yaml

│     service.yaml

│     ingress.yaml

│     configmap.yaml

│     secret.yaml

│     NOTES.txt

│     _helpers.tpl

└── .helmignore
```

---

# 7. Chart.yaml

Contains metadata.

Example

```yaml
apiVersion: v2
name: nginx
description: Nginx Helm Chart
type: application
version: 1.0.0
appVersion: "1.25"
```

---

# 8. values.yaml

Stores configurable values.

Example

```yaml
replicaCount: 2

image:
  repository: nginx
  tag: latest

service:
  type: ClusterIP
  port: 80
```

---

# 9. Templates

Templates generate Kubernetes YAML dynamically.

Example

```yaml
replicas: {{ .Values.replicaCount }}
```

Output

```
replicas: 2
```

---

# 10. Template Functions

Examples

```
default

quote

upper

lower

trim

replace

printf

indent

nindent

toYaml

fromYaml

b64enc

b64dec
```

Example

```yaml
{{ upper .Values.name }}
```

---

# 11. Built-in Objects

```
.Values

.Chart

.Release

.Files

.Capabilities

.Template
```

Example

```
{{ .Release.Name }}
```

---

# 12. Helpers (_helpers.tpl)

Reusable templates.

Example

```yaml
{{- define "mychart.fullname" -}}

{{ .Release.Name }}

{{- end }}
```

Call

```yaml
{{ include "mychart.fullname" . }}
```

---

# 13. Variables

```
{{ $name := .Values.name }}
```

Use

```
{{ $name }}
```

---

# 14. Conditional Statements

```
{{ if .Values.enabled }}

...

{{ end }}
```

If Else

```
{{ if }}

{{ else }}

{{ end }}
```

---

# 15. Loops

```
{{ range .Values.ports }}

- {{ . }}

{{ end }}
```

---

# 16. Pipelines

```
{{ .Values.name | upper | quote }}
```

---

# 17. Default Values

```
{{ default "nginx" .Values.image }}
```

---

# 18. Named Templates

```
{{ define "labels" }}

...

{{ end }}
```

---

# 19. Include vs Template

Include

```
{{ include "labels" . }}
```

Returns string.

Template

```
{{ template "labels" . }}
```

Writes directly into output.

---

# 20. Files Directory

Read file

```
{{ .Files.Get "config.txt" }}
```

---

# 21. ConfigMap

Example

```yaml
apiVersion: v1
kind: ConfigMap
```

---

# 22. Secret

Example

```yaml
apiVersion: v1
kind: Secret
type: Opaque
```

---

# 23. Deployment

Usually contains

- Image
- Replica
- Labels
- Container Port
- Resources
- Liveness Probe
- Readiness Probe

---

# 24. Service

Types

- ClusterIP
- NodePort
- LoadBalancer
- ExternalName

---

# 25. Ingress

Routes external traffic into the cluster.

---

# 26. Hooks

Lifecycle hooks

```
pre-install

post-install

pre-delete

post-delete

pre-upgrade

post-upgrade

pre-rollback

post-rollback
```

---

# 27. Helm Lifecycle

```
Create Chart

↓

Install

↓

Upgrade

↓

Rollback

↓

Delete
```

---

# 28. Dependencies

Chart.yaml

```yaml
dependencies:

- name: redis
  version: 18.0.0
  repository: https://charts.bitnami.com/bitnami
```

Update

```
helm dependency update
```

---

# 29. Helm Repository

Add

```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

Update

```
helm repo update
```

Search

```
helm search repo nginx
```

---

# 30. Packaging

```
helm package mychart
```

Creates

```
mychart-1.0.0.tgz
```

---

# 31. Versioning

Chart Version

```
version
```

Application Version

```
appVersion
```

---

# 32. Upgrade

```
helm upgrade myapp .
```

---

# 33. Rollback

History

```
helm history myapp
```

Rollback

```
helm rollback myapp 2
```

---

# 34. Uninstall

```
helm uninstall myapp
```

---

# 35. Debugging

```
helm lint .

helm template .

helm install --dry-run .

helm install --debug .
```

---

# 36. Linting

```
helm lint mychart
```

Checks

- YAML syntax
- Best practices
- Template issues

---

# 37. Best Practices

✅ Keep values configurable

✅ Never hardcode image tags

✅ Use helpers

✅ Use labels consistently

✅ Keep secrets outside Git

✅ Use semantic versioning

✅ Validate with helm lint

✅ Test using dry-run

✅ Keep templates reusable

---

# 38. Helm Interview Questions

### What is Helm?

Package manager for Kubernetes.

---

### What is a Helm Chart?

A collection of Kubernetes YAML templates.

---

### What is values.yaml?

Stores user-configurable values.

---

### Difference between include and template?

include returns string.

template writes output directly.

---

### What is _helpers.tpl?

Reusable template definitions.

---

### How do you rollback?

```
helm rollback RELEASE REVISION
```

---

### How to see release history?

```
helm history RELEASE
```

---

### How to debug Helm?

```
helm lint

helm template

helm install --dry-run

helm install --debug
```

---

### Helm Workflow

```
Create Chart

↓

Modify values.yaml

↓

Update Templates

↓

helm lint

↓

helm template

↓

helm install

↓

helm upgrade

↓

helm rollback

↓

helm uninstall
```

---

# Useful Commands Cheat Sheet

```
helm version

helm create mychart

helm lint .

helm template .

helm install app .

helm list

helm status app

helm get values app

helm history app

helm upgrade app .

helm rollback app 1

helm uninstall app

helm repo add

helm repo update

helm search repo

helm dependency update

helm package .
```

---

# References

- Kubernetes Official Documentation
- Helm Official Documentation
- CNCF Helm Project

---

⭐ If this repository helps you, don't forget to give it a Star!