# Helm + ArgoCD + CI/CD Interview Questions and Answers

---

# SECTION 1 — HELM INTERVIEW QUESTIONS

## 1. What is Helm?
Helm is a Kubernetes package manager used to deploy and manage applications using Helm Charts.

## 2. What is a Helm Chart?
A collection of Kubernetes YAML manifests packaged together.

## 3. What is a Helm Release?
An installed instance of a chart in a cluster.

## 4. Helm v2 vs Helm v3
- Helm v3 removed Tiller
- More secure
- Uses kubeconfig directly

## 5. Important Helm Commands

```
helm install myapp ./chart
helm upgrade myapp ./chart
helm rollback myapp 1
helm uninstall myapp
helm list
```

## 6. values.yaml Purpose
Stores default configuration values.

## 7. Helm Templating
Uses Go templates:

```
replicas: {{ .Values.replicaCount }}
```

## 8. Helm Hooks
Lifecycle triggers:

- pre-install
- post-install
- pre-upgrade

## 9. Helm Dependencies
Supports sub‑charts via Chart.yaml.

## 10. Helm Security Best Practices

- Use Helm v3
- Signed charts
- Secret management
- RBAC

---

# SECTION 2 — HELM + ARGOCD INTERVIEW QUESTIONS

## 11. What is Argo CD?
Argo CD is a GitOps continuous delivery tool for Kubernetes.

It syncs Kubernetes clusters with Git repositories.

---

## 12. How Helm Works with Argo CD?

Argo CD can deploy Helm charts directly from:

- Git repos
- Helm repos
- OCI registries

Argo CD renders Helm templates and applies manifests.

---

## 13. Argo CD Helm Deployment Flow

1. Developer updates Helm chart in Git
2. Argo CD detects Git change
3. Helm templates rendered
4. Kubernetes manifests applied
5. Sync status updated

---

## 14. Example Argo CD Application with Helm

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: helm-app
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/org/repo.git
    targetRevision: main
    path: helm-chart
    helm:
      valueFiles:
        - values.yaml
  destination:
    server: https://kubernetes.default.svc
    namespace: prod
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

---

## 15. Difference: Helm CLI vs Argo CD Helm

| Helm CLI | Argo CD |
|----------|---------|
| Manual deploy | GitOps deploy |
| CLI driven | Declarative |
| Local execution | Controller based |
| No drift detection | Drift detection |

---

## 16. Can Argo CD Override values.yaml?

Yes.

Using:

- values.yaml
- valueFiles
- parameters
- Helm set overrides

---

## 17. Helm Repo vs Git Repo in Argo CD

| Helm Repo | Git Repo |
|-----------|----------|
| Packaged charts | Source charts |
| Versioned tgz | Raw templates |
| Faster pulls | More flexible |

---

## 18. Benefits of Helm + Argo CD

- GitOps workflow
- Version control
- Automated sync
- Easy rollback
- Multi‑env promotion

---

# SECTION 3 — HELM IN CI/CD PIPELINES

## 19. How Helm is Used in CI/CD?

Typical pipeline:

1. Build image
2. Push to registry
3. Update Helm values
4. Deploy via Helm / Argo CD

---

## 20. Sample CI/CD Flow with Helm

```
Git Commit → CI Build → Docker Push →
Update values.yaml → Deploy via Helm
```

---

## 21. Jenkins Pipeline Example

```groovy
stage('Deploy') {
  steps {
    sh 'helm upgrade --install myapp ./chart         --set image.tag=${BUILD_NUMBER}'
  }
}
```

---

## 22. GitHub Actions + Helm Example

```yaml
- name: Deploy to Kubernetes
  run: |
    helm upgrade --install myapp ./chart       --set image.tag=${{ github.sha }}
```

---

## 23. Azure DevOps + Helm

```yaml
- task: HelmDeploy@0
  inputs:
    command: upgrade
    chartType: FilePath
    chartPath: charts/myapp
    releaseName: myapp
```

---

## 24. Image Tag Automation in Helm

Update dynamically:

```
--set image.tag=1.0.${BUILD_ID}
```

Or via values file update.

---

## 25. Helm Rollback in CI/CD

```
helm rollback myapp 2
```

Used during failed deployments.

---

## 26. Promotion Across Environments

Helm supports:

- dev-values.yaml
- qa-values.yaml
- prod-values.yaml

---

## 27. Secrets Management in Helm Pipelines

Tools used:

- Kubernetes Secrets
- HashiCorp Vault
- AWS Secrets Manager
- SOPS + Helm Secrets

---

## 28. Helm Testing

```
helm test myapp
```

Runs test pods defined in chart.

---

## 29. Linting in CI

```
helm lint ./chart
```

Validates chart syntax.

---

## 30. Packaging & Publishing via CI

```
helm package chart
helm push chart.tgz repo
```

---

# SECTION 4 — SCENARIO‑BASED QUESTIONS

## 31. How do you deploy same app to multiple clusters?

Using:

- Argo CD ApplicationSets
- Helm values per cluster

---

## 32. Blue‑Green Deployment with Helm

- Two releases
- Switch service selector

---

## 33. Canary Deployment

- Adjust replica weights
- Service mesh (Istio/Linkerd)

---

## 34. How to handle config drift?

Argo CD auto‑sync + self‑heal.

---

## 35. How do you rollback failed GitOps deployment?

Revert Git commit → Argo CD sync.

---

# END OF DOCUMENT
