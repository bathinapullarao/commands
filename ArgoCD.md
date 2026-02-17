# Argo CD Interview Questions & Answers (2026)

> Format: **Question** followed by a crisp **Answer**.  
> Focus: real-world GitOps, Argo CD architecture, security, multi-cluster, troubleshooting, and best practices.
>  argocd app get <app-name>  
argocd app status <app-name>  
argocd app diff <app-name>  
argocd app sync <app-name>  
argocd app refresh <app-name> --hard  <--Hard refresh when cache/state looks stale  
---

## 1) What is Argo CD?

**Answer:**  
Argo CD is a **Kubernetes-native GitOps continuous delivery** tool. It watches Git repositories (desired state) and ensures the live cluster state matches Git by continuously comparing and optionally syncing changes.

---

## 2) What problem does Argo CD solve?

**Answer:**  
It solves **configuration drift**, manual deployments, and inconsistent environments by making Git the **single source of truth** for Kubernetes manifests/Helm/Kustomize and automating reconciliation.

---

## 3) Explain GitOps in your own words.

**Answer:**  
GitOps means:
- Desired state is stored in **Git**
- Changes happen via **pull request / review**
- Deployment is performed by an **agent in the cluster**
- The agent continuously **reconciles** live state to match Git

---

## 4) What are the main Argo CD components?

**Answer:**  
- **argocd-server**: API/UI, handles RBAC and user interactions  
- **repo-server**: fetches and renders manifests (Helm/Kustomize)  
- **application-controller**: compares live vs desired and performs sync  
- **redis** (often): caching for performance  
- Optional: **dex** (SSO), **notifications controller**, **application-set controller**

---

## 5) What is an Argo CD Application?

**Answer:**  
An Application is a CRD that defines:
- **source** (repo URL, path/chart, revision)
- **destination** (cluster API server + namespace)
- **sync policy** (manual/automated, prune, self-heal)
- **health & sync status**

---

## 6) What is the difference between Sync and Refresh?

**Answer:**  
- **Refresh**: Argo re-checks Git and/or cluster state to recompute diff/status.
- **Sync**: Argo applies changes to the cluster to match Git (kubectl apply under the hood).

---

## 7) What is “drift” and how does Argo CD handle it?

**Answer:**  
Drift occurs when live state changes outside Git (kubectl edit, manual apply). Argo detects drift via diff and:
- Shows it as **OutOfSync**
- Optionally **self-heals** (if automated sync + selfHeal is enabled)

---

## 8) What is Automated Sync? What are prune and selfHeal?

**Answer:**  
- **Automated sync**: Argo auto-applies changes when Git updates.  
- **prune**: deletes resources removed from Git.  
- **selfHeal**: reverts manual changes in the cluster back to Git state.

---

## 9) What is a Sync Wave?

**Answer:**  
Sync waves control apply order using annotations like:
`argocd.argoproj.io/sync-wave: "0"`, `"1"`, etc.  
Lower waves apply first (useful for CRDs, namespaces, RBAC before apps).

---

## 10) How does Argo CD decide resource ordering?

**Answer:**  
Argo sorts by:
1. **Sync waves** (if provided)
2. **Resource kind order** (namespaces/CRDs before CRs, etc.)
3. Dependencies and internal heuristics

---

## 11) What is a “Project” in Argo CD?

**Answer:**  
An **AppProject** is a security boundary to restrict:
- allowed repos
- allowed destinations (clusters/namespaces)
- allowed resource kinds
- cluster-scoped resource permissions  
It’s used for **multi-team governance**.

---

## 12) How do you manage multiple clusters with Argo CD?

**Answer:**  
Register clusters in Argo CD (as secrets) and set each Application destination server to that cluster. Use:
- **AppProjects** to restrict access
- **ApplicationSet** for templated multi-cluster deployments

---

## 13) What is ApplicationSet and why is it used?

**Answer:**  
ApplicationSet generates many Applications from a template using generators like:
- Git directory generator
- list generator
- cluster generator
- matrix/merge generators  
Great for **multi-cluster** or **multi-tenant** scaling.

---

## 14) Helm vs Kustomize vs plain YAML in Argo CD — when to use what?

**Answer:**  
- **Plain YAML**: simple, explicit, stable config.
- **Kustomize**: overlays per env (dev/stage/prod), no templating.
- **Helm**: complex parameterized apps, chart ecosystems, versioning.

---

## 15) How does Argo CD authenticate to Git repos?

**Answer:**  
Via repository credentials:
- HTTPS + username/token (PAT)
- SSH key-based auth  
Credentials are stored as Kubernetes secrets in `argocd` namespace (or external secret managers).

---

## 16) How does Argo CD handle secrets?

**Answer:**  
Best practice: **do not store raw secrets in Git**. Use:
- **Sealed Secrets**
- **External Secrets Operator**
- **Vault / cloud KMS**
- **SOPS** with KMS and Argo CD integration (decrypt at deploy time)

---

## 17) What is RBAC in Argo CD? Where is it configured?

**Answer:**  
Argo CD RBAC is typically configured via `argocd-rbac-cm` ConfigMap using:
- roles
- policies
- groups mapping  
You can integrate with SSO (Dex/OIDC) and map groups to roles.

---

## 18) How do you integrate SSO (OIDC/SAML) with Argo CD?

**Answer:**  
Commonly:
- Use **Dex** (built-in connector) or direct OIDC config
- Configure identity provider (Azure AD/Okta/Google)
- Map groups/claims to Argo roles via RBAC

---

## 19) What is “resource pruning” risk and how do you mitigate it?

**Answer:**  
Prune can delete resources unexpectedly if Git state is wrong. Mitigations:
- Enable prune only for mature apps
- Use manual sync first for risky changes
- Protect critical resources with `argocd.argoproj.io/sync-options: Prune=false`
- Use AppProject restrictions

---

## 20) What are Sync Options?

**Answer:**  
Per-resource or per-app options using annotations:
- `ApplyOutOfSyncOnly=true`
- `Prune=false`
- `Replace=true`
- `CreateNamespace=true`
- `Validate=false` (use carefully)
- `ServerSideApply=true` (in newer setups)

---

## 21) How do you handle CRDs safely in Argo CD?

**Answer:**  
- Apply CRDs first (sync wave)
- Separate CRDs into a dedicated Application
- Use `SkipDryRunOnMissingResource=true` for CRs that depend on CRDs (carefully)

---

## 22) What causes an Application to show “OutOfSync”?

**Answer:**  
Typical causes:
- Git changed but not applied
- Live state modified manually
- Helm/Kustomize rendered output differs
- Different image tags or mutated fields by controllers (HPA, admission webhooks)

---

## 23) What is “Healthy” vs “Degraded”?

**Answer:**  
Health is computed using built-in or custom health checks:
- **Healthy**: resources are running/available as expected
- **Degraded**: failures (CrashLoopBackOff, unavailable deployment, failed jobs)
- **Progressing**: rollout in progress

---

## 24) How do you troubleshoot a stuck sync?

**Answer:**  
Steps:
- Check Application events in UI
- Inspect controller logs: `application-controller`
- Look for failing resource apply, RBAC denies, webhooks errors
- Verify repo-server rendering (helm/kustomize errors)
- Confirm cluster connectivity/permissions

---

## 25) Where do you check manifest generation errors?

**Answer:**  
In **repo-server logs** and the Application status message. Often due to:
- Helm template errors
- missing values files
- Kustomize build failures
- private repo auth issues

---

## 26) How do you do blue/green or canary with Argo CD?

**Answer:**  
Argo CD handles desired state; progressive delivery is usually done with:
- **Argo Rollouts** (recommended)
- or service selector/ingress changes with separate manifests  
Argo CD deploys the Rollout resources; Rollouts controls traffic shifting.

---

## 27) What is Argo Rollouts (in one line)?

**Answer:**  
A Kubernetes controller for **progressive delivery** (canary/blue-green) with metrics-based promotion/rollback.

---

## 28) How do you promote an image version with GitOps?

**Answer:**  
Update Git (PR) to change:
- image tag/digest
- helm values
- kustomize image patch  
Then Argo CD syncs. For automation use image update tools:
- Argo CD Image Updater (common)
- or CI pipeline commit (safer with approvals)

---

## 29) What is the best practice for image tags?

**Answer:**  
Prefer **immutable digests** or versioned tags (e.g., `1.2.3`) over `latest`. It improves reproducibility and rollback.

---

## 30) How do you prevent Argo CD from overwriting fields mutated by controllers?

**Answer:**  
Use:
- `ignoreDifferences` in Application spec (JSON pointers/jq path)
- resource customizations in `argocd-cm`  
This is common for fields like `replicas` (HPA), webhook-injected annotations, etc.

---

## 31) What is “orphaned resources” in Argo CD?

**Answer:**  
Resources in the cluster not tracked by Argo CD (not in Git or not part of app). Argo can detect orphans depending on settings.

---

## 32) How do you delete an application safely?

**Answer:**  
- If you want to remove resources: delete Application with **cascade** (and prune)  
- If you want to keep resources: disable prune/cascade or adjust finalizers accordingly

---

## 33) What is “App of Apps” pattern?

**Answer:**  
A parent Application points to a directory of child Application manifests. It helps manage many apps consistently via a single root app.

---

## 34) How do you structure repos for Argo CD?

**Answer:**  
Common patterns:
- **mono-repo**: `apps/`, `clusters/`, `environments/`
- **multi-repo**: app repo + separate env/config repo  
Keep clear environment overlays and avoid duplication.

---

## 35) How do you restrict what namespaces an app can deploy into?

**Answer:**  
Use **AppProject** destination restrictions (`destinations`) and RBAC. Avoid giving broad cluster-admin to Argo.

---

## 36) How does Argo CD connect to the Kubernetes API?

**Answer:**  
Argo runs in cluster and uses:
- in-cluster credentials for the local cluster
- cluster credentials stored as secrets for external clusters  
It needs RBAC permissions to apply/monitor resources.

---

## 37) What is a common security hardening checklist for Argo CD?

**Answer:**  
- Enable SSO + RBAC least privilege
- Restrict repos and destinations with AppProjects
- Use HTTPS, rotate repo credentials
- Limit cluster-admin; use per-namespace roles
- Audit logs + monitor controller actions
- Avoid plain secrets in Git; use SOPS/External Secrets

---

## 38) What is “sync window”?

**Answer:**  
A feature to allow/deny syncs for apps/projects during specific times (change freeze windows).

---

## 39) How do you roll back with Argo CD?

**Answer:**  
Rollback is usually done by:
- Reverting Git commit (preferred)
- Using application history/rollback feature (if enabled), which effectively syncs to a previous revision

---

## 40) What is the difference between Argo CD and Flux?

**Answer:**  
Both are GitOps CD tools. Common differences:
- Argo CD is known for a strong UI and Application model
- Flux is more composable with multiple controllers and native Kustomize focus  
Both can achieve similar outcomes; choice depends on org preference.

---

## 41) How do you handle database migrations in Argo CD?

**Answer:**  
Use Kubernetes Jobs or Helm hooks carefully; recommended patterns:
- Separate migration Job with sync wave before app deploy
- Make migrations idempotent
- Monitor job health and set proper sync options

---

## 42) What are “hooks” in Argo CD?

**Answer:**  
Argo supports hooks via annotations (PreSync/Sync/PostSync) to run Jobs or other resources at specific points in the sync lifecycle.

---

## 43) How do you debug “permission denied” during sync?

**Answer:**  
Check:
- Kubernetes RBAC for Argo service account
- AppProject restrictions
- Cluster registration credentials
- Namespace existence and permissions  
Also inspect controller logs for forbidden errors.

---

## 44) How do you migrate apps between clusters?

**Answer:**  
- Register new cluster in Argo CD
- Update Application destination server/namespace
- Ensure prerequisites (namespaces, CRDs, RBAC) exist
- Sync and validate health, then decommission old destination

---

## 45) What are common causes of “ComparisonError”?

**Answer:**  
- Repo auth issues
- manifest generation failures
- invalid YAML/Helm render errors
- API server connectivity issues
- unknown resource kinds (CRDs missing)

---

## 46) How do you scale Argo CD for many applications?

**Answer:**  
- Increase controller replicas (HA)
- Use redis (HA)
- Tune reconciliation settings
- Use ApplicationSets to reduce manual overhead
- Split Argo instances by team/environment if needed

---

## 47) What does “Health check customization” mean?

**Answer:**  
You can define custom health rules (often Lua) for how Argo determines health for certain kinds (especially CRDs).

---

## 48) How does Argo CD handle Helm values?

**Answer:**  
You can specify:
- `helm.valueFiles`
- `helm.parameters`
- `helm.values`  
Argo renders templates in repo-server and applies the output to the cluster.

---

## 49) What is the difference between “targetRevision” and “path”?

**Answer:**  
- **targetRevision**: Git branch/tag/commit (or chart version)
- **path**: directory containing manifests/helm chart/kustomize base

---

## 50) Give a short example Argo CD Application (skeleton).

**Answer:**  
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: sample
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/org/repo.git
    targetRevision: main
    path: apps/sample
  destination:
    server: https://kubernetes.default.svc
    namespace: sample
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

---

## Quick “Real Interview” Scenarios (short answers)

### A) “Prod should never auto-sync. How will you do it?”
**Answer:** Use manual sync in prod apps, enforce via AppProject policies, and use sync windows to block unexpected syncs.

### B) “We need dev auto-sync but no pruning.”
**Answer:** Enable automated sync but set prune false via `syncOptions: [Prune=false]`.

### C) “HPA keeps changing replicas and Argo marks OutOfSync.”
**Answer:** Configure `ignoreDifferences` for `spec.replicas` on the Deployment.

### D) “We have 50 clusters; how to deploy same app everywhere?”
**Answer:** Use **ApplicationSet** cluster generator + templating.

---

## Suggested topics to mention in interviews
- AppProjects for governance
- SOPS/External Secrets for secrets
- ApplicationSet for scale
- Argo Rollouts for canary/blue-green
- ignoreDifferences to reduce noise
- sync waves + hooks for ordering and migrations

---

*End of document.*
