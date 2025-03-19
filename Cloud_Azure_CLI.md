## How to mount Blob storage as a file system with blobfuse
yum install blobfuse
sudo mount -t tmpfs -o size=16g tmpfs /mnt/ramdisk

Azure offers a vast range of services, but here are the most widely used categories and services based on their use cases:

1️⃣ Compute Services (Virtual Machines & Serverless)
🔹 Azure Virtual Machines (VMs) – Run Windows/Linux VMs for applications
🔹 Azure Kubernetes Service (AKS) – Managed Kubernetes for containerized apps
🔹 Azure Functions – Serverless compute to run event-driven workloads
🔹 Azure App Service – Deploy and manage web apps, APIs, and mobile backends
🔹 Azure Container Instances (ACI) – Run containers without managing servers

2️⃣ Storage & Database Services
🔹 Azure Blob Storage – Object storage for large-scale unstructured data
🔹 Azure Files – Managed file shares in the cloud
🔹 Azure SQL Database – Managed relational database with auto-scaling
🔹 Azure Cosmos DB – NoSQL database for high-performance global apps
🔹 Azure Data Lake – Big data storage for analytics workloads

3️⃣ Networking Services
🔹 Azure Virtual Network (VNet) – Private networking in Azure
🔹 Azure Load Balancer – Distribute traffic across multiple VMs
🔹 Azure Application Gateway – Layer 7 load balancing with Web Application Firewall (WAF)
🔹 Azure ExpressRoute – Private, dedicated connections to Azure
🔹 Azure VPN Gateway – Secure hybrid cloud connectivity

4️⃣ Identity & Security
🔹 Azure Active Directory (Azure AD) – Identity & access management for users and apps
🔹 Azure Key Vault – Securely store and manage secrets, keys, and certificates
🔹 Microsoft Defender for Cloud – Security posture management and threat protection
🔹 Azure Firewall – Cloud-native firewall with threat intelligence
🔹 Azure DDoS Protection – Protect apps from distributed denial-of-service attacks

5️⃣ DevOps & Monitoring
🔹 Azure DevOps – CI/CD, source control, and agile project management
🔹 Azure Monitor – Collect, analyze, and visualize logs and metrics
🔹 Azure Log Analytics – Advanced logging and querying for insights
🔹 Azure Automation – Automate processes, patching, and runbooks
🔹 Azure Application Insights – Monitor and diagnose application performance

6️⃣ AI, Machine Learning & Analytics
🔹 Azure Machine Learning – Build and deploy ML models
🔹 Azure Cognitive Services – Pre-built AI models for vision, speech, and language
🔹 Azure Synapse Analytics – Data warehousing and analytics at scale
🔹 Azure Databricks – Managed Apache Spark for big data analytics
🔹 Azure Stream Analytics – Real-time data processing

7️⃣ Internet of Things (IoT)
🔹 Azure IoT Hub – Connect and manage IoT devices
🔹 Azure IoT Central – Fully managed IoT solution
🔹 Azure Digital Twins – Create digital replicas of real-world objects
🔹 Azure Time Series Insights – Analyze IoT data in real-time

8️⃣ Hybrid & Multi-Cloud
🔹 Azure Arc – Manage on-premises and multi-cloud environments
🔹 Azure Stack – Run Azure services on-premises
🔹 Azure Backup – Cloud-based backup solution
🔹 Azure Site Recovery – Disaster recovery and business continuity

9️⃣ Messaging & Event-Driven Services
🔹 Azure Service Bus – Enterprise-grade messaging between applications
🔹 Azure Event Grid – Event-driven orchestration for applications
🔹 Azure Event Hubs – Stream large-scale event data in real-time
🔹 Azure Notification Hubs – Send push notifications to mobile devices

10️⃣ Management & Governance
🔹 Azure Policy – Enforce organizational compliance policies
🔹 Azure Cost Management – Monitor and optimize cloud spending
🔹 Azure Blueprints – Deploy standardized cloud environments
🔹 Azure Resource Manager (ARM) – Manage infrastructure as code (IaC)

Most Popular Use Cases for Azure Services
✅ Web & Mobile Apps – App Service, Functions, Cosmos DB
✅ Big Data & Analytics – Synapse, Databricks, Data Lake
✅ Hybrid Cloud & Security – Azure AD, Azure Arc, Key Vault
✅ DevOps & Automation – Azure DevOps, Terraform, ARM Templates
✅ IoT & AI/ML – IoT Hub, Machine Learning, Cognitive Services


# Azure CLI 2.0 Cheatsheet

Azure CLI 2.0 cheatsheet for Login, Resources, VMs, Resource groups, Storage, Batch, and Containers.

## Logging in

### Login with web
```
az login
```

### Login in CLI
```
az login -u myemail@address.com
```

### List accounts
```
az account list
```

### Set subscription
```
az account set --subscription "xxx"
```

## Listing locations and resources / general

### List all locations
```
az account list-locations
```

### List all my resource groups
```
az resource list
```

### Get what version of the CLI you have
```
azure --version
```

### Get help
```
azure help
```

## Creating a basic VM / Resource Group / Storage Account

### Get all available VM sizes
```
az vm list-sizes --location eastus
```

### Get all available VM images for Windows and Linux
```
az vm image list --output table
```

### Create a Linux VM
```
az vm create --resource-group myResourceGroup --name myVM --image ubuntults
```

### Create a Windows VM
```
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter
```

### Create a Resource group
```
az group create --name myresourcegroup --location eastus
```

### Create a Storage account.
```
az storage account create -g myresourcegroup -n mystorageaccount -l eastus --sku Standard_LRS
```

## DELETING A RESOURCE GROUP

### Permanetly deletes a resource group
```
az group delete --name myResourceGroup
```

## Managing VM's

### List your VMs
```
az vm list
```

### Start a VM
```
az vm start --resource-group myResourceGroup --name myVM
```

### Stop a VM
```
az vm stop --resource-group myResourceGroup --name myVM
```

### Deallocate a VM
```
az vm deallocate --resource-group myResourceGroup --name myVM
```

### Restart a VM
```
az vm restart --resource-group myResourceGroup --name myVM
```

### Redeploy a VM
```
az vm redeploy --resource-group myResourceGroup --name myVM
```

### Delete a VM
```
az vm delete --resource-group myResourceGroup --name myVM
```

### Create image of a VM
```
az image create --resource-group myResourceGroup --source myVM --name myImage
```

### Create VM from image
```
az vm create --resource-group myResourceGroup --name myNewVM --image myImage
```

### List VM extensions
```
az vm extension list --resource-group azure-playground-resources --vm-name azure-playground-vm
```

### Delete VM extensions
```
az vm extension delete --resource-group azure-playground-resources --vm-name azure-playground-vm --name bootstrapper
```

## Managing Batch Account

### Create a Batch account.
```
az batch account create -g myresourcegroup -n mybatchaccount -l eastus
```

### Create a Storage account.
```
az storage account create -g myresourcegroup -n mystorageaccount -l eastus --sku Standard_LRS
```

### Associate Batch with storage account.
```
az batch account set -g myresourcegroup -n mybatchaccount --storage-account mystorageaccount
```

We can now authenticate directly against the account for further CLI interaction.

```
az batch account login -g myresourcegroup -n mybatchaccount
```

### Display the details of our created account.
```
az batch account show -g myresourcegroup -n mybatchaccount
```

### Create a new application.
```
az batch application create --resource-group myresourcegroup --name mybatchaccount --application-id myapp --display-name "My Application"
```

### Add zip files to application
```
az batch application package create --resource-group myresourcegroup --name mybatchaccount --application-id myapp --package-file my-application-exe.zip --version 1.0
```

### Assign the application package as the default version.
```
az batch application set --resource-group myresourcegroup --name mybatchaccount --application-id myapp --default-version 1.0
```

### Retrieve a list of available images and node agent SKUs.
```
az batch pool node-agent-skus list
```

### Create new Linux pool with VM config
```
az batch pool create \
    --id mypool-linux \
    --vm-size Standard_A1 \
    --image canonical:ubuntuserver:16.04.0-LTS \
    --node-agent-sku-id “batch.node.ubuntu 16.04”
```

### Now let's resize the pool to start up some VMs.
```
az batch pool resize --pool-id mypool-linux --target-dedicated 5
```

### We can check the status of the pool to see when it has finished resizing.
```
az batch pool show --pool-id mypool-linux
```

### List the compute nodes running in a pool.
```
az batch node list --pool-id mypool-linux
```

If a particular node in the pool is having issues, it can be rebooted or reimaged.
A typical node ID will be in the format 'tvm-xxxxxxxxxx_1-<timestamp>'.
```
az batch node reboot --pool-id mypool-linux --node-id tvm-123_1-20170316t000000z
```

### Re-allocate work to another node.
```
az batch node delete \
    --pool-id mypool-linux \
    --node-list tvm-123_1-20170316t000000z tvm-123_2-20170316t000000z \
    --node-deallocation-option requeue
```

### Create a new job to encapsulate the tasks that we want to add.
```
az batch job create --id myjob --pool-id mypool
```

### Add tasks to the job.
 …where <shell> is your preferred shell for execution (/bin/sh, /bin/bash, /bin/ksh etc.), and /path/to/script.sh is, of course, the full path of the shell script you’re invoking to get things started.

```
az batch task create --job-id myjob --task-id task1 --application-package-references myapp#1.0 --command-line "/bin/<shell> -c /path/to/script.sh"
```

### Add many tasks at once
```
az batch task create --job-id myjob --json-file tasks.json
```

Now that all the tasks are added - we can update the job so that it will automatically be marked as completed once all the tasks are finished.

```
az batch job set --job-id myjob --on-all-tasks-complete terminateJob
```

### Monitor the status of the job.
```
az batch job show --job-id myjob
```

### Monitor the status of a task.
```
az batch task show --job-id myjob --task-id task1
```

### Delete a job
```
az batch job delete --job-id myjob
```

## Managing Containers

If you HAVE AN SSH run this to create an Azure Container Service Cluster (~10 mins)

```
az acs create -n acs-cluster -g acsrg1 -d applink789
```

If you DO NOT HAVE AN SSH run this to create an Azure Container Service Cluster (~10 mins)

```
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

### List clusters under your whole subscription
```
az acs list --output table
```

### List clusters in a resource group
```
az acs list -g acsrg1 --output table
```

### Display details of a container service cluster
```
az acs show -g acsrg1 -n acs-cluster --output list
```

### Scale using ACS
```
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

### Delete a cluster
```
az acs delete -g acsrg1 -n acs-cluster
```
