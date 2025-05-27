
**<ins>AWS:</ins>** 
```  
login to AWS console and go to iam create secteate key access key,
provide access to services to it.create vpc with multiple subnets and another vpc,
create vpc peering,create a bastion server and connect from it to all the servers.
create elastic ip's, assign to ec2 instance, create gke cluster, ec2 instance,
AWS lambda,s3 buckets,rds,route53 or cloud flare, update SSL certificates,
understand about security groups and network acl's
```
**<ins>GCP:</ins>**  
```
login to gcp console, create Iam user, security groups , provide access,
create compute engine,instance group, gke, all ingress some ports in firewall,
create cloudsql, vpc, vpc peering, tunneling to windows
```
**<ins>AZURE:</ins>** 
```
login to azure console, create security principle, active directory,azure DevOps,
vm's, aks
```
# Cloud Service Comparison: AWS vs. GCP vs. Azure

## 1️⃣ Compute Services
| Feature                 | AWS (Amazon Web Services) | GCP (Google Cloud Platform) | Azure (Microsoft Azure) |
|-------------------------|--------------------------|----------------------------|-------------------------|
| **Virtual Machines**   | EC2 (Elastic Compute Cloud) | Compute Engine | Virtual Machines (VMs) |
| **Auto Scaling**       | Auto Scaling Groups | Managed Instance Groups | Virtual Machine Scale Sets |
| **Serverless Compute** | AWS Lambda | Cloud Functions | Azure Functions |
| **Container Orchestration** | EKS (Elastic Kubernetes Service) | GKE (Google Kubernetes Engine) | AKS (Azure Kubernetes Service) |
| **Container Service**  | ECS (Elastic Container Service), Fargate | Cloud Run | Azure Container Instances (ACI) |
| **Bare Metal Servers** | AWS Bare Metal | Bare Metal Solution | Azure Bare Metal |

## 2️⃣ Storage Services
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Object Storage** | S3 (Simple Storage Service) | Cloud Storage (GCS) | Blob Storage |
| **Block Storage** | EBS (Elastic Block Store) | Persistent Disks | Managed Disks |
| **File Storage** | EFS (Elastic File System) | Filestore | Azure Files |
| **Cold Storage** | S3 Glacier | Coldline Storage | Archive Storage |
| **Hybrid Storage** | AWS Storage Gateway | Transfer Appliance | Azure StorSimple |

## 3️⃣ Networking Services
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Load Balancer** | ELB (Elastic Load Balancer) | Cloud Load Balancer | Azure Load Balancer |
| **CDN (Content Delivery)** | CloudFront | Cloud CDN | Azure CDN |
| **VPC (Virtual Private Cloud)** | Amazon VPC | VPC | Azure Virtual Network (VNet) |
| **Hybrid Connectivity** | AWS Direct Connect | Cloud Interconnect | ExpressRoute |
| **DNS Service** | Route 53 | Cloud DNS | Azure DNS |

## 4️⃣ Database Services
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Managed SQL Database** | RDS (Relational Database Service) | Cloud SQL | Azure SQL Database |
| **NoSQL Database** | DynamoDB | Firestore, Bigtable | Cosmos DB |
| **Data Warehouse** | Redshift | BigQuery | Synapse Analytics |
| **Cache Service** | ElastiCache (Redis, Memcached) | Memorystore (Redis) | Azure Cache for Redis |
| **Graph Database** | Neptune | N/A | Azure Cosmos DB (Gremlin API) |

## 5️⃣ Identity & Security
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **IAM (Identity & Access Management)** | AWS IAM | Google IAM | Azure AD, RBAC |
| **Key Management** | AWS KMS | Cloud KMS | Azure Key Vault |
| **DDoS Protection** | AWS Shield | Cloud Armor | Azure DDoS Protection |
| **Security Services** | AWS Security Hub | Security Command Center | Microsoft Defender for Cloud |

## 6️⃣ AI & Machine Learning
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **AI/ML Platform** | SageMaker | Vertex AI | Azure ML |
| **Speech-to-Text** | Amazon Transcribe | Speech-to-Text | Azure Speech |
| **Text-to-Speech** | Polly | Text-to-Speech | Azure Speech |
| **Computer Vision** | Rekognition | Vision AI | Azure Computer Vision |
| **AI Chatbots** | Lex | Dialogflow | Azure Bot Service |

## 7️⃣ DevOps & Monitoring
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **CI/CD Pipeline** | CodePipeline | Cloud Build | Azure DevOps |
| **Monitoring** | CloudWatch | Cloud Monitoring | Azure Monitor |
| **Logging** | CloudTrail | Cloud Logging | Azure Log Analytics |
| **Infrastructure as Code** | CloudFormation | Deployment Manager | ARM Templates / Bicep |
| **Secrets Management** | AWS Secrets Manager | Secret Manager | Azure Key Vault |

## 8️⃣ Hybrid & Multi-Cloud
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Hybrid Cloud Management** | Outposts | Anthos | Azure Arc |
| **VM Migration** | AWS VM Import/Export | Migrate for Compute Engine | Azure Migrate |
| **Kubernetes Hybrid** | EKS Anywhere | GKE On-Prem | AKS Hybrid |

## 9️⃣ Big Data & Analytics
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Big Data Processing** | EMR (Elastic MapReduce) | Dataproc | Azure HDInsight |
| **Stream Processing** | Kinesis | Dataflow | Azure Stream Analytics |
| **Data Warehouse** | Redshift | BigQuery | Azure Synapse |
| **Event Processing** | AWS EventBridge | Pub/Sub | Event Grid |

## 🔟 Pricing & Billing
| Feature          | AWS | GCP | Azure |
|-----------------|-----|-----|-------|
| **Billing Model** | Pay-as-you-go | Pay-as-you-go | Pay-as-you-go |
| **Free Tier** | 12 months free | Always Free with limits | 12 months free |
| **Per-Second Billing** | Yes | Yes | Yes |

## 📝 Summary: Which Cloud Provider is Best?
| Category | Best Provider |
|----------|--------------|
| **Compute (VMs, Containers)** | **AWS & GCP** (Best performance) |
| **Serverless (Functions)** | **AWS Lambda** (Mature) |
| **AI/ML** | **GCP** (Best AI tools) |
| **Networking (CDN, VPC)** | **AWS** (Best Global Reach) |
| **Storage** | **Azure & AWS** |
| **Databases** | **AWS & Azure** (Largest variety) |
| **Big Data** | **GCP** (BigQuery is fastest) |
| **Hybrid Cloud** | **Azure (Azure Arc)** |

## **🔍 Comparison: GKE vs. EKS vs. AKS vs. Self-Managed Kubernetes**

| Feature | **GKE (Google Kubernetes Engine)** | **EKS (Elastic Kubernetes Service - AWS)** | **AKS (Azure Kubernetes Service)** | **Self-Managed Kubernetes (K8s on VM/Bare Metal)** |
|---------|-----------------------------------|--------------------------------------------|------------------------------------|----------------------------------------|
| **Control Plane** | Fully managed by Google | Managed by AWS | Managed by Azure | Self-managed (Manual Setup) |
| **Node Management** | Uses **Node Pools** | Uses **Node Groups** | Uses **Node Pools** | Fully manual |
| **Scaling** | Auto Node Scaling, Cluster Autoscaler | Cluster Autoscaler, Karpenter | Cluster Autoscaler | Manual scaling |
| **Load Balancing** | Native **Google Cloud Load Balancer** | **AWS ALB/NLB** | **Azure Load Balancer** | Needs external setup (NGINX, MetalLB, etc.) |
| **Storage** | Persistent Disks (GCE PD) | EBS, EFS | Azure Disks, Azure Files | Needs manual configuration |
| **Networking** | **VPC-Native** (uses Google Cloud VPC) | **VPC CNI** (Elastic Network Interface) | **Azure CNI** or Kubenet | Manual setup (Calico, Flannel, Cilium) |
| **Security & IAM** | **GCP IAM** (OIDC, Workload Identity) | **AWS IAM Roles for Service Accounts (IRSA)** | **Azure AD** (MS Entra ID) | Manual RBAC setup |
| **Ingress** | Native **Cloud Load Balancer** | ALB Ingress Controller | Application Gateway Ingress | Needs external setup (NGINX, Traefik) |
| **Pricing** | Control Plane free, Pay for nodes | $0.10/hour for Control Plane + Worker Nodes | Control Plane free, Pay for nodes | No extra costs (but infra costs apply) |
| **Ease of Use** | 🟢 **Easiest** (Deep GCP integration) | 🔵 **Moderate** (IAM & networking complexity) | 🟣 **Moderate** (Azure AD integration) | 🔴 **Hard** (Full manual management) |
| **Multi-Cloud Support** | ❌ No | ❌ No | ❌ No | ✅ Yes (Can run on any cloud or on-prem) |
| **Ideal Use Case** | **Best for AI/ML, Big Data, and Google Cloud users** | **Best for AWS-heavy workloads and enterprises** | **Best for Azure users & hybrid workloads** | **Best for on-prem or multi-cloud Kubernetes** |

---
**Domain name**  
```
Let’s say you bought a domain: example.com from GoDaddy.  
By default, DNS queries for example.com go to GoDaddy’s name servers.  
After setting up Cloud DNS, Google gives you **name servers** like:  
ns-cloud-a1.googledomains.com  
ns-cloud-a2.googledomains.com  
ns-cloud-a3.googledomains.com  
ns-cloud-a4.googledomains.com  
You go to your GoDaddy dashboard and replace the default name servers with the ones above.
```  
➡️~~Result:~~ Now, whenever someone looks up example.com, DNS queries are sent to Google Cloud DNS instead of GoDaddy.  


# 🧪You can allow access only to specific IPs or domains and block the rest.
## Method 1:  
```  
**Step 1:** Allow access to specific domains (e.g., example.com)  
iptables -A OUTPUT -p tcp -d example.com --dport 80 -j ACCEPT  
iptables -A OUTPUT -p tcp -d example.com --dport 443 -j ACCEPT  
ptables -A OUTPUT -p tcp -d 93.184.216.34 --dport 443 -j ACCEPT  
dig +short example.com  
**Step 2:** Block all other traffic  
iptables -A OUTPUT -p tcp --dport 80 -j DROP  
iptables -A OUTPUT -p tcp --dport 443 -j DROP  
⚠️ Make sure SSH (port 22) and DNS (53) are not blocked if you're connected remotely.
```  
## Method 2:  
Using a Proxy (Squid)  
```  
You can install a proxy like Squid and configure it to allow specific sites.  
sudo apt install squid -y  
sudo nano /etc/squid/squid.conf  
acl allowed_sites dstdomain .example.com .another-site.com  
http_access allow allowed_sites  
http_access deny all  
sudo systemctl restart squid
```  
## Method 3:  
/etc/hosts Blocking (Not Secure), You can override DNS resolution for blocking, not ideal for strict security:  
```   
sudo nano /etc/hosts  
Add lines to block sites by redirecting to localhost:   
127.0.0.1  facebook.com  
127.0.0.1  youtube.com
```  
## Method 4:  
Use ufw (Simpler Firewall)  
``` 
If using ufw:  
sudo ufw default deny outgoing  
sudo ufw allow out to 93.184.216.34 port 443 proto tcp  
sudo ufw allow out to 8.8.8.8 port 53 proto udp  # for DNS
``` 
># 🧰 Linux Network-Related Commands Cheat Sheet


## 🔧 Basic Commands

| Command | Description |
|--------|-------------|
| **`ip a`** or `ip addr` | Shows all network interfaces and their IP addresses |
| **`telnet 192.168.1.10 22`** | Check if port 22 is open on 192.168.1.10 |
| `nmap -p 80 192.168.1.10`| Check if port 80 is open on 192.168.1.10 |
| `nc -zv 192.168.1.10 443` | netcat Check if port 443 is open on 192.168.1.10, -z = scan without sending data,-v = verbose output |
| `ip r` or `ip route` | Shows the routing table (default gateway, routes) |
| `ip link` | Shows and manages network interfaces |
| **`ping <host>`** | Tests connectivity to another host (ICMP echo) |
| **`traceroute <host>`** | Shows the path packets take to a destination |
| **`nslookup <domain>`** | Queries DNS to resolve domain names |
| **`dig <domain>`** | Advanced DNS lookup tool, "dig ANY example.com", ANY requests all available record types |
| **`hostname`** | Displays or sets the system hostname |
| `hostname -I` | Shows the system’s IP address |
| **`ifconfig`** *(deprecated)* | Shows and configures network interfaces (use `ip` instead) |
| **`netstat -tuln`** | Shows listening ports and services (use `ss` in modern systems) |
| **`ss -tuln`** | Faster alternative to `netstat`, shows open ports and services |
| **`nmap <IP or range>`** | Scans ports on a target host (requires installation) |
| `curl <URL>` | Performs HTTP requests from the command line |
| `wget <URL>` | Downloads files from the web |
| `ethtool eth0` | Displays settings of a network interface (replace `eth0` with interface name) |
| `tcpdump -i eth0` | Captures network packets on interface `eth0` (requires root) |
| `nmcli` | Command-line tool for NetworkManager configuration |
| `ip neigh` | Shows ARP table (neighbor cache) |
| `arp -a` | Shows ARP entries (used in local LAN mapping) |
| **`route -n`** | Displays kernel routing table (older tool; `ip route` is preferred) |

---

## 🧪 Practical Usage Examples
```bash
# Show current IP address
ip a
# Check internet connectivity
ping 8.8.8.8
```

# 🔐 Places to Write Access Policies in AWS

In **AWS**, you can write access policies in various places depending on what you're securing and who/what needs access.

---

## ✅ Places You Can Write Access Policies

| **Place** | **Description** | **Scope** | **Policy Type** |
|-----------|------------------|-----------|------------------|
| **IAM User** | Attached directly to a user | Single user | Identity-based |
| **IAM Group** | Policies attached to a group; affect all members | Group of users | Identity-based |
| **IAM Role** | Used by services, users, or federated identities | Service or trusted entity | Identity-based |
| **Resource-based Policy** | Attached directly to a resource (e.g., S3 bucket) | Specific resource | Resource-based |
| **Service Control Policy (SCP)** | Part of AWS Organizations; controls what accounts can do | Entire account or OU | Organization policy |
| **Session Policies** | Temporary permissions in STS AssumeRole sessions | Session duration | Identity-based |
| **Permissions Boundary** | Limits the maximum permissions an IAM role or user can have | IAM entity level | Boundary policy |
| **Access Control Lists (ACLs)** | Legacy; controls access to S3 buckets and objects | Resource-specific | Resource access |
| **VPC Endpoint Policies** | Control access through VPC endpoints | Network path-level | Resource-based |
| **Bucket Policies (S3)** | Specific to S3 buckets | Per bucket | Resource-based |
| **Lambda Resource Policies** | Controls who can invoke your Lambda | Per function | Resource-based |
| **KMS Key Policies** | Manage access to encryption keys | Per key | Resource-based |
| **SQS/SNS/Lake Formation/Secrets Manager Policies** | Specific to these services | Per resource | Resource-based |
| **IAM Policy Simulator** | Tool to test policies, not a policy location | N/A | N/A |

---

## 🧠 Policy Types in AWS

| **Type** | **Attached To** | **Controls** |
|----------|------------------|---------------|
| **Identity-based policy** | IAM users, groups, roles | What actions they can perform on which resources |
| **Resource-based policy** | AWS resources like S3, Lambda, KMS | Who can access the resource and how |
| **SCP (Org-level)** | AWS accounts or Organizational Units | Max permissions boundary |
| **Permissions boundary** | IAM roles/users | Limit maximum effective permissions |
| **Session policy** | STS sessions | Temporary fine-grained access control |

---

## 🔒 Example: Controlling Access to an S3 Bucket

- **IAM Policy on User:**  
  Allows `s3:PutObject` on `my-bucket`.

- **Bucket Policy:**  
  Allows public `s3:GetObject` on all objects in the bucket.

- **Permissions Boundary:**  
  Limits user from doing anything outside of `s3:GetObject`.

---

## ✅ Recommendations

- Use **IAM roles** for EC2, Lambda, etc.
- Use **resource-based policies** for shared services like S3, KMS, SNS.
- Use **SCPs** to restrict permissions across accounts in AWS Organizations.
- Use **permissions boundaries** for delegation of admin capabilities.

---

![Screenshot of a comment on a GitHub issue showing an image, added in the Markdown, of an Octocat smiling and raising a tentacle.](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQk_6_iIAWFIm6OKoeUek1i9IypLrLMJ8jOPA&s)
![gif file](https://barreirofisica.wordpress.com/wp-content/uploads/2013/06/albert-einstein.gif)
