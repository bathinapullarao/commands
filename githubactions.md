# GitHub Actions to Deploy to GKE --- Full Explanation

## 1. CI/CD Flow Overview

This guide explains how GitHub Actions connects to: - GitHub
repository - Google Cloud - GKE Kubernetes cluster - Artifact Registry\
and performs full CI/CD deployment.

## 2. Workflow Trigger

``` yaml
on:
  push:
    branches: [ "main" ]
```

Pipeline runs whenever a push happens on the **main** branch.

## 3. Checkout Code from GitHub

``` yaml
uses: actions/checkout@v3
```

GitHub downloads your repository inside the workflow runner.

## 4. Authenticate to Google Cloud

``` yaml
uses: google-github-actions/auth@v2
with:
  credentials_json: ${{ secrets.GCP_SA_KEY }}
```

This loads your GCP service account JSON from GitHub Secrets and logs
into Google Cloud.

### After this step, the pipeline can:

-   Access GKE cluster\
-   Push images to Artifact Registry\
-   Run gcloud / kubectl commands

## 5. Install gcloud CLI

``` yaml
uses: google-github-actions/setup-gcloud@v2
```

Installs the Google Cloud SDK.

## 6. Configure Docker for Artifact Registry

``` yaml
gcloud auth configure-docker REGION-docker.pkg.dev
```

This allows Docker to push images into Artifact Registry without
username/password.

## 7. Build & Push Docker Image

``` yaml
IMAGE="REGION-docker.pkg.dev/PROJECT/repo/app:${{ github.sha }}"
docker build -t $IMAGE .
docker push $IMAGE
```

GitHub Actions: 1. Builds Docker image\
2. Tags it using commit SHA\
3. Pushes to GCP Artifact Registry

## 8. Connect to GKE Cluster

``` yaml
gcloud container clusters get-credentials CLUSTER_NAME --region REGION --project PROJECT_ID
```

This step downloads kubeconfig and connects kubectl to your GKE cluster.

After this, GitHub Actions **can run kubectl commands** directly on the
cluster.

## 9. Deploy to Kubernetes

``` yaml
kubectl set image deployment/myapp myapp-container=$IMAGE
kubectl rollout status deployment/myapp
```

Kubernetes pulls the new Docker image and updates the running
application.

## 10. Full CI/CD Summary

  -----------------------------------------------------------------------
  Step            Connection                      Purpose
  --------------- ------------------------------- -----------------------
  GitHub → GitHub Trigger workflow                Start CI/CD
  Actions                                         

  GitHub Actions  Checkout code                   Get application source
  → Repo                                          

  GitHub Actions  Authenticate                    Access resources
  → GCP                                           

  GitHub Actions  Docker login                    Push images
  → Artifact                                      
  Registry                                        

  GitHub Actions  Get cluster credentials         Deploy
  → GKE                                           

  GitHub Actions  kubectl apply/set image         Update app
  → Kubernetes                                    
  API                                             
  -----------------------------------------------------------------------

## Final Result

✔ Fully automated CI/CD\
✔ Build → Push → Deploy → Rollout\
✔ Zero-downtime deployment to GKE
