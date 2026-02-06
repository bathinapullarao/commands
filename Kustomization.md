# How to Deploy Applications Using Kustomization

---

## What is Kustomization?

Kustomize is a Kubernetes native configuration management tool that allows you to customize Kubernetes manifests **without modifying the original YAML files**.

Customizations are defined in:

kustomization.yaml

It supports:

- Patching resources
- Image tag overrides
- Namespace changes
- ConfigMap & Secret generation
- Environment overlays

---

# Directory Structure Example

kustomize-app/
 ├── base/
 │    ├── deployment.yaml
 │    ├── service.yaml
 │    └── kustomization.yaml
 │
 └── overlays/
      ├── dev/
      │    └── kustomization.yaml
      └── prod/
           └── kustomization.yaml

---

# Step 1 — Create Base Manifests

## deployment.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - name: myapp
        image: nginx:latest

---

## service.yaml

apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector:
    app: myapp
  ports:
  - port: 80

---

## base/kustomization.yaml

resources:
  - deployment.yaml
  - service.yaml

---

# Step 2 — Create Overlay (Environment Customization)

## overlays/dev/kustomization.yaml

resources:
  - ../../base

namePrefix: dev-

namespace: dev

replicas:
  - name: myapp
    count: 2

images:
  - name: nginx
    newTag: 1.25

---

# Step 3 — Deploy Using kubectl

Deploy Dev:

kubectl apply -k overlays/dev

Deploy Prod:

kubectl apply -k overlays/prod

---

# Step 4 — Render YAML (Dry Run)

kubectl kustomize overlays/dev

OR

kustomize build overlays/dev

---

# Deploy Using Argo CD

Argo CD auto-detects Kustomize if kustomization.yaml is present.

---

## Argo CD Application Example

apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: kustomize-app
  namespace: argocd
spec:
  project: default

  source:
    repoURL: https://github.com/org/repo.git
    targetRevision: main
    path: overlays/prod

  destination:
    server: https://kubernetes.default.svc
    namespace: prod

  syncPolicy:
    automated:
      prune: true
      selfHeal: true

---

# Deployment Flow

Git Repo → Argo CD → Kustomize Build → kubectl apply → Deployment

---

# Interview One‑Line Answer

Kustomize deploys applications using kustomization.yaml to customize base Kubernetes manifests and deploy via kubectl apply -k or Argo CD.

---

# End of Document
