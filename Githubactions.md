# GitHub Actions Interview Questions and Answers

## 1. What is GitHub Actions?
GitHub Actions is a CI/CD automation platform built into GitHub that allows you to automate build, test, and deployment workflows directly from your repository.

Workflows are defined using YAML files stored in:
```
.github/workflows/
```

---

## 2. Main Components of GitHub Actions

| Component | Description |
|-----------|-------------|
| Workflow | Automated process defined in YAML |
| Event | Trigger (push, PR, schedule) |
| Job | Group of steps running on same runner |
| Step | Individual task |
| Action | Reusable unit of code |
| Runner | Machine that executes jobs |

---

## 3. What is a Runner?
A runner is a server that executes workflows.

Types:
- GitHub-hosted runners
- Self-hosted runners

---

## 4. Workflow File Location
```
.github/workflows/workflow-name.yml
```

---

## 5. Common Workflow Triggers
- push
- pull_request
- workflow_dispatch
- schedule
- release

Example:
```yaml
on:
  push:
    branches: [ main ]
```

---

# Intermediate Questions

## 6. What is an Action?
Reusable automation component.

Example:
```yaml
- uses: actions/checkout@v4
```

---

## 7. Difference Between Job and Step

| Job | Step |
|-----|------|
| Runs on runner | Runs inside job |
| Parallel | Sequential |

---

## 8. Passing Data Between Jobs
Using outputs or artifacts.

---

## 9. Secrets in GitHub Actions
Encrypted variables used for credentials.

Access:
```yaml
${{ secrets.AWS_ACCESS_KEY_ID }}
```

---

# CI/CD Pipeline

## 10. Simple CI Workflow
```yaml
name: CI Pipeline

on:
  push:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test
```

---

## 11. Docker Build Example
```yaml
- run: docker build -t myapp:latest .
- run: docker push myrepo/myapp:latest
```

---

## 12. Cache Dependencies
```yaml
- uses: actions/cache@v4
  with:
    path: ~/.npm
    key: npm-${{ hashFiles('package-lock.json') }}
```

---

# Advanced Questions

## 13. Matrix Builds
```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest]
```

---

## 14. Environment Approvals
Configured in GitHub Environments for manual approvals.

---

## 15. OIDC Authentication
Secure cloud authentication without storing secrets.

---

## 16. Artifacts
Upload build outputs.

```yaml
- uses: actions/upload-artifact@v4
```

---

# Kubernetes Deployment

## 17. Deploy to Kubernetes
Steps:
1. Build image
2. Push registry
3. Apply manifests

```yaml
kubectl apply -f deployment.yaml
```

---

# GitHub Actions vs Jenkins

| Feature | GitHub Actions | Jenkins |
|--------|----------------|---------|
| Setup | Built-in | External |
| Maintenance | Low | High |

---

# Troubleshooting

## 18. Workflow Not Triggering
Common issues:
- YAML errors
- Wrong branch
- File path incorrect

---

## 19. Debugging Workflows
- Enable debug logs
- Check runner logs

---

# Scenario Questions

## 20. End-to-End CI/CD Flow
1. Code push  
2. Build  
3. Test  
4. Scan  
5. Docker build  
6. Deploy  

---

# Rapid Fire

| Question | Answer |
|---------|--------|
| Manual trigger? | workflow_dispatch |
| File format? | YAML |
| Default runner? | Ubuntu |

---

## 16. Central Reusable Workflow
```yaml
devops-pipelines-repo
   └── .github/workflows/microservice-ci.yml   (Reusable workflow)

service-user-repo
   └── .github/workflows/ci.yml                (Calls reusable workflow)

service-payment-repo
   └── .github/workflows/ci.yml                (Calls reusable workflow)
```
Repository: devops-pipelines-repo
.github/workflows/microservice-ci.yml

```yaml
name: Reusable Microservice CI

on:
  workflow_call:
    inputs:
      service_name:
        required: true
        type: string
      docker_image:
        required: true
        type: string
      environment:
        required: true
        type: string

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Show variables
        run: |
          echo "Service Name: ${{ inputs.service_name }}"
          echo "Docker Image: ${{ inputs.docker_image }}"
          echo "Environment: ${{ inputs.environment }}"

      - name: Build Docker Image
        run: |
          docker build -t ${{ inputs.docker_image }} .

      - name: Push Docker Image
        run: |
          echo "Pushing image ${{ inputs.docker_image }}"

  deploy:
    runs-on: ubuntu-latest
    needs: build

    steps:
      - name: Deploy
        run: |
          echo "Deploying ${{ inputs.service_name }} to ${{ inputs.environment }}"
```
Microservice Repo Workflow

Example repo: user-service

.github/workflows/ci.yml

```yaml
name: User Service CI

on:
  push:
    branches:
      - main

jobs:
  call-reusable-workflow:

    uses: my-org/devops-pipelines-repo/.github/workflows/microservice-ci.yml@main

    with:
      service_name: user-service
      docker_image: myrepo/user-service:latest
      environment: dev
```
Another Microservice Example

Example repo: payment-service
```yaml
name: Payment Service CI

on:
  push:
    branches:
      - main

jobs:
  call-reusable-workflow:

    uses: my-org/devops-pipelines-repo/.github/workflows/microservice-ci.yml@main

    with:
      service_name: payment-service
      docker_image: myrepo/payment-service:latest
      environment: prod
```
Passing Secrets

If you need secrets (like registry credentials):

Reusable workflow:
```yaml
on:
  workflow_call:
    secrets:
      docker_password:
        required: true
```

Caller workflow:
```yaml
jobs:
  call-reusable-workflow:
    uses: my-org/devops-pipelines-repo/.github/workflows/microservice-ci.yml@main

    with:
      service_name: user-service
      docker_image: myrepo/user-service:latest
      environment: dev

    secrets:
      docker_password: ${{ secrets.DOCKER_PASSWORD }}
```
Using Repository Variables Automatically

If each repo has variables:
```yaml
Settings → Variables → Actions
Example:

SERVICE_NAME=user-service
ENVIRONMENT=dev

Then workflow becomes:

with:
  service_name: ${{ vars.SERVICE_NAME }}
  docker_image: myrepo/${{ vars.SERVICE_NAME }}:latest
  environment: ${{ vars.ENVIRONMENT }}
```
Enterprise Pattern (Recommended)
```yaml
org
 ├── devops-workflows-repo
 │      └ reusable-ci.yml
 │
 ├── service1
 ├── service2
 ├── service3
 └── service42
```
