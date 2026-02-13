```  yaml
✅ 1. Prerequisites
On GCP:
✔️ A GKE cluster
✔️ A service account with these roles:
roles/container.admin
roles/storage.admin
roles/artifactregistry.admin
roles/iam.serviceAccountUser

✔️ Enable required APIs:
gcloud services enable container.googleapis.com artifactregistry.googleapis.com

✔️ Download service account JSON (example: gke-sa.json)

✅ 2. Store Secrets in GitHub
Go to:GitHub Repo → Settings → Secrets and variables → Actions → New Repository Secret
Create:
Secret Name	Value
GCP_PROJECT_ID	your GCP project
GKE_CLUSTER_NAME	your cluster name
GKE_REGION	e.g., asia-south1 / us-central1
GCP_SA_KEY	copy service account JSON content

✅ 3. Create Artifact Registry (Optional, for Docker images)
gcloud artifacts repositories create myrepo \
--repository-format=docker \
--location=asia-south1

Example image path:
asia-south1-docker.pkg.dev/PROJECT_ID/myrepo/myapp

You must create the file ".github/workflows/gke-deploy.yml" inside your project repository, in a very specific path.

Here is the exact required location:

myapp/
 ├── Dockerfile
 ├── app.py
 ├── k8s/
 ├── README.md
 └── .github/
      └── workflows/
           └── gke-deploy.yml

##The file .github/workflows/gke-deploy.yml executes automatically inside GitHub when certain events happen — you do NOT run it manually.

✅ 4. Create GitHub Actions Workflow
Create file:
.github/workflows/gke-deploy.yml
```

#Paste this YAML:
```  yaml
name: Deploy to GKE

on:
  push:
    branches: [ "main" ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Authenticate to Google Cloud
      uses: google-github-actions/auth@v2
      with:
        credentials_json: ${{ secrets.GCP_SA_KEY }}

    - name: Set up gcloud CLI
      uses: google-github-actions/setup-gcloud@v2

    - name: Configure Docker for Artifact Registry
      run: gcloud auth configure-docker ${{ secrets.GKE_REGION }}-docker.pkg.dev

    - name: Build & Push Docker Image
      run: |
        IMAGE="${{ secrets.GKE_REGION }}-docker.pkg.dev/${{ secrets.GCP_PROJECT_ID }}/myrepo/myapp:${{ github.sha }}"
        docker build -t $IMAGE .
        docker push $IMAGE
        echo "IMAGE_NAME=$IMAGE" >> $GITHUB_ENV

    - name: Get GKE Credentials
      run: |
        gcloud container clusters get-credentials ${{ secrets.GKE_CLUSTER_NAME }} \
        --region ${{ secrets.GKE_REGION }} \
        --project ${{ secrets.GCP_PROJECT_ID }}

    - name: Deploy to GKE using kubectl
      run: |
        kubectl set image deployment/myapp myapp-container=${IMAGE_NAME}
        kubectl rollout status deployment/myapp

```

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

``` yaml
name: Deploy Helm to EKS

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1 # Update to your region

      - name: Install kubectl
        uses: azure/setup-kubectl@v4

      - name: Install Helm
        uses: azure/setup-helm@v4
        with:
          version: 'latest'

      - name: Update kubeconfig
        run: aws eks update-kubeconfig --name your-cluster-name --region us-east-1

      - name: Deploy Helm chart
        run: |
          helm upgrade --install my-release-name ./helm-chart-directory --namespace my-namespace --create-namespace
```
