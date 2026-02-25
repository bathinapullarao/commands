# Oracle OCI Interview Questions and Answers

## 1. What is Oracle Cloud Infrastructure (OCI)?

Oracle Cloud Infrastructure (OCI) is Oracle's cloud platform that
provides IaaS, PaaS, and SaaS services. It offers compute, storage,
networking, databases, security, and monitoring services with high
performance and enterprise-grade security.

------------------------------------------------------------------------

## 2. What are the core services in OCI?

-   Compute (VMs, Bare Metal)
-   Block Storage
-   Object Storage
-   VCN (Virtual Cloud Network)
-   Load Balancer
-   Autonomous Database
-   IAM (Identity and Access Management)
-   Monitoring and Logging

------------------------------------------------------------------------

## 3. What is a Compartment in OCI?

A compartment is a logical container used to organize and isolate
resources within a tenancy. Access to resources is controlled using IAM
policies at the compartment level.

------------------------------------------------------------------------

## 4. What is VCN in OCI?

VCN (Virtual Cloud Network) is a customizable private network in OCI,
similar to AWS VPC or Azure VNet. It includes subnets, route tables,
security lists, gateways, and DHCP options.

------------------------------------------------------------------------

## 5. Difference between Security List and Network Security Group (NSG)?

Security List: - Applied at subnet level. - Controls ingress and egress
traffic.

NSG: - Applied at instance level. - Provides fine-grained security
control.

------------------------------------------------------------------------

## 6. What are the types of storage in OCI?

-   Block Storage: Persistent disk for compute instances.
-   Object Storage: Scalable storage for unstructured data.
-   File Storage: Shared file system (NFS).
-   Archive Storage: Low-cost long-term storage.

------------------------------------------------------------------------

## 7. What is Autonomous Database?

Autonomous Database is a self-managing, self-securing, and
self-repairing Oracle database service that automates patching, tuning,
backups, and scaling.

------------------------------------------------------------------------

## 8. What is Fault Domain and Availability Domain?

Availability Domain (AD): - A data center within a region.

Fault Domain (FD): - A grouping of hardware and infrastructure within an
AD to provide high availability.

------------------------------------------------------------------------

## 9. How does IAM work in OCI?

OCI IAM controls access using: - Users - Groups - Dynamic Groups -
Policies Policies define permissions using a statement like: Allow group
DevOps to manage instances in compartment ProjectA

------------------------------------------------------------------------

## 10. What is Dynamic Group in OCI?

Dynamic Groups allow compute instances to access OCI services using
instance principals without storing credentials.

------------------------------------------------------------------------

## 11. What is Load Balancer in OCI?

OCI Load Balancer distributes traffic across backend servers. It
supports: - Public and Private Load Balancer - Layer 4 and Layer 7
routing

------------------------------------------------------------------------

## 12. What is OCI Object Storage Tiering?

OCI provides: - Standard Tier (Hot storage) - Infrequent Access Tier -
Archive Tier (Cold storage)

------------------------------------------------------------------------

## 13. What is Terraform in OCI?

Terraform is used to provision OCI infrastructure as code using OCI
provider.

Example:

``` hcl
provider "oci" {
  region = "ap-mumbai-1"
}
```

------------------------------------------------------------------------

## 14. What is Instance Principal?

Instance Principal allows a compute instance to authenticate with OCI
services using IAM policies without API keys.

------------------------------------------------------------------------

## 15. How do you monitor resources in OCI?

Using: - OCI Monitoring Service - Alarms - Logging - Events Service

------------------------------------------------------------------------

# DevOps Scenario-Based Questions

## 16. How do you deploy an application in OCI?

-   Create VCN and Subnets
-   Launch Compute Instances
-   Configure Security Lists / NSG
-   Install application
-   Configure Load Balancer
-   Enable Monitoring

------------------------------------------------------------------------

## 17. How do you secure OCI resources?

-   Use IAM least privilege policies
-   Enable MFA
-   Use Vault for secrets
-   Configure NSG rules
-   Enable audit logging

------------------------------------------------------------------------

## 18. How do you achieve High Availability in OCI?

-   Deploy across multiple Availability Domains
-   Use Fault Domains
-   Configure Load Balancer
-   Enable Auto Scaling

------------------------------------------------------------------------

## 19. What is OCI Vault?

OCI Vault securely stores encryption keys and secrets. It integrates
with other OCI services.

------------------------------------------------------------------------

## 20. What is Auto Scaling in OCI?

Auto Scaling automatically adjusts the number of compute instances based
on CPU or memory metrics.

------------------------------------------------------------------------

# Oracle OCI -- Advanced & Architect Level Interview Q&A (Complete Guide)

------------------------------------------------------------------------

# ✅ Advanced Scenario‑Based OCI Questions

## 1. How do you design HA architecture in OCI?

Deploy workloads across multiple Availability Domains, use Fault
Domains, place instances behind a Load Balancer, enable Auto Scaling,
and configure DR replication.

## 2. Your public subnet instances cannot access the internet. What do you check?

-   Internet Gateway
-   Route Table (0.0.0.0/0 → IGW)
-   Security Lists / NSG rules
-   Public IP assignment

## 3. Private subnet needs outbound internet access?

Use **NAT Gateway** with route table entry.

## 4. On‑premises connectivity options?

-   Site‑to‑Site VPN
-   FastConnect
-   IPSec VPN

## 5. Block Volume performance issue troubleshooting?

-   Check VPUs
-   Instance shape limits
-   Multipath enabled
-   Volume attachment type

## 6. DR strategy for databases?

Use Data Guard, Autonomous DB cross‑region backup, Object Storage
replication.

## 7. Secure secrets for apps?

Use **OCI Vault + Secrets + Dynamic Groups**.

## 8. Cost optimization scenario?

-   Use Auto Scaling
-   Reserved Capacity
-   Right‑size shapes
-   Archive Storage

## 9. Multi‑tier app network design?

-   Web → Public Subnet
-   App → Private Subnet
-   DB → Isolated Subnet

## 10. Zero downtime deployment?

Use Blue/Green with Load Balancer backend switch.

------------------------------------------------------------------------

# ✅ OCI Architect‑Level Questions

## 11. Explain OCI Tenancy architecture.

Tenancy → Compartments → VCN → Subnets → Resources.

## 12. Design multi‑region DR.

Primary + Secondary region replication + DNS failover.

## 13. Hub‑and‑Spoke networking?

Use DRG + VCN peering.

## 14. When to use Service Gateway?

Private access to OCI PaaS services.

## 15. IAM best practices?

Least privilege, dynamic groups, federation.

## 16. Design secure 3‑tier architecture?

WAF → LB → App → DB with NSGs.

## 17. Storage selection strategy?

Block (DB), Object (backup), File (shared apps), Archive (long
retention).

## 18. Migration strategy to OCI?

Rehost, Replatform, Refactor.

## 19. Logging & audit architecture?

OCI Logging + Service Connector Hub → Object Storage/SIEM.

## 20. Enterprise landing zone design?

Compartments, IAM federation, budget alerts, guardrails.

------------------------------------------------------------------------

# ✅ OCI + DevOps CI/CD Interview Q&A

## 21. CI/CD tools in OCI?

-   OCI DevOps
-   Jenkins
-   GitHub Actions
-   GitLab

## 22. Artifact storage?

OCI Artifact Registry / Object Storage.

## 23. Build pipeline flow?

Code → Build → Test → Image → Push → Deploy.

## 24. Container deployment target?

OKE (Oracle Kubernetes Engine).

## 25. Secrets in pipeline?

OCI Vault integration.

## 26. Rolling deployment in OKE?

Kubernetes RollingUpdate strategy.

## 27. Blue/Green in OCI?

Load Balancer backend sets.

## 28. Infra provisioning in CI/CD?

Terraform + OCI provider.

## 29. Monitoring pipeline?

OCI Logging + Notifications.

## 30. DevSecOps in OCI?

Vulnerability scanning + Vault + IAM.

------------------------------------------------------------------------

# ✅ OCI + Terraform Full Examples

## Provider Configuration

``` hcl
provider "oci" {
  region = "ap-mumbai-1"
}
```

------------------------------------------------------------------------

## Create VCN

``` hcl
resource "oci_core_vcn" "main_vcn" {
  cidr_block = "10.0.0.0/16"
  display_name = "main-vcn"
  compartment_id = var.compartment_id
}
```

------------------------------------------------------------------------

## Create Subnet

``` hcl
resource "oci_core_subnet" "public_subnet" {
  cidr_block = "10.0.1.0/24"
  vcn_id = oci_core_vcn.main_vcn.id
  compartment_id = var.compartment_id
  display_name = "public-subnet"
}
```

------------------------------------------------------------------------

## Launch Compute Instance

``` hcl
resource "oci_core_instance" "vm" {
  availability_domain = var.ad
  compartment_id      = var.compartment_id
  shape               = "VM.Standard.E4.Flex"

  create_vnic_details {
    subnet_id = oci_core_subnet.public_subnet.id
  }

  source_details {
    source_type = "image"
    source_id   = var.image_id
  }

  display_name = "demo-vm"
}
```

------------------------------------------------------------------------

## Block Volume

``` hcl
resource "oci_core_volume" "block" {
  availability_domain = var.ad
  compartment_id      = var.compartment_id
  size_in_gbs         = 50
}
```

------------------------------------------------------------------------

# ✅ 100+ OCI Interview Questions (Rapid Fire)

### Core Services

31. What is OCI?
32. Regions vs AD?
33. Fault Domains?
34. Compartments?
35. Tags?

### Compute

36. Shapes?
37. Bare Metal vs VM?
38. Preemptible instances?
39. Custom images?
40. Instance pools?

### Storage

41. Block vs Object?
42. File Storage?
43. Archive tier?
44. Backup policies?
45. Cross‑region replication?

### Networking

46. VCN?
47. Subnets?
48. Route tables?
49. IGW?
50. NAT Gateway?
51. Service Gateway?
52. DRG?
53. LPG?
54. NSG vs Security List?
55. Private IP vs Public IP?

### IAM

56. Users?
57. Groups?
58. Policies?
59. Dynamic groups?
60. Federation?

### Databases

61. Autonomous DB?
62. Exadata?
63. Data Guard?
64. Backup strategy?
65. Scaling?

### Kubernetes / Containers

66. OKE?
67. Node pools?
68. Autoscaling?
69. Ingress?
70. Helm?

### DevOps

71. OCI DevOps service?
72. Build pipelines?
73. Deployment pipelines?
74. Artifact Registry?
75. Notifications?

### Security

76. Vault?
77. WAF?
78. Shield?
79. Cloud Guard?
80. Security Zones?

### Monitoring

81. Metrics?
82. Alarms?
83. Logging?
84. Events?
85. Notifications?

### Migration

86. Lift & Shift?
87. Database migration?
88. Storage transfer?
89. Hybrid cloud?
90. DR drills?

### Cost

91. Budgets?
92. Cost analysis?
93. Reserved capacity?
94. Autoscaling savings?
95. Storage tiering savings?

### Architecture / Advanced

96. Landing zone?
97. Multi‑region failover?
98. Hub‑spoke design?
99. Zero trust model?
100. Enterprise IAM design?
101. DR automation?
102. Compliance architecture?
103. Backup vaulting?
104. Edge security?
105. Observability stack?

------------------------------------------------------------------------


