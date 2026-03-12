# Azure Fundamentals Summary

---

## 1. What is Cloud Computing?

Cloud computing means using someone else's computers and infrastructure over the internet, provided by cloud vendors like Microsoft Azure, AWS, or Google Cloud. Instead of buying physical servers, you rent resources and pay only for what you use — this is called the **pay-as-you-go model**.

### Three Service Models

| Model | Full Name | What the Provider Gives You | Example |
|---|---|---|---|
| **IaaS** | Infrastructure as a Service | Virtual machines, storage, networking — raw infrastructure | Renting a VM on Azure to install your own software |
| **PaaS** | Platform as a Service | A ready platform to build and deploy apps without managing servers | Using Azure App Service to host a web application |
| **SaaS** | Software as a Service | A fully built software product accessed via browser or app | Using Microsoft 365 (Word, Outlook) without installing anything |

---

## 2. How Azure is Organized

Azure uses a four-level hierarchy to manage resources, control access, and track costs.

```
Tenant
  └── Subscription
        └── Resource Group
              └── Resource
```

**Tenant** — The top-level identity of your organization in Azure. Think of it as the name and identity of your company registered with Microsoft. Every organization has one tenant.

**Subscription** — Sits inside the tenant. It is the billing boundary — all costs for resources inside a subscription are tracked and billed together. A company can have multiple subscriptions (e.g., one for dev, one for production).

**Resource Group** — A logical container inside a subscription used to organize related resources. For example, the IT department may have its own resource group, and the HR department may have another. This makes it easy to manage, monitor, and delete related resources together.

**Resource** — The actual cloud service being used, such as a Virtual Machine, a Storage Account, or a database. Every resource lives inside a resource group.

**Why this hierarchy matters:** It gives organizations clear control over who can access what (access control) and how costs are tracked per team or project (billing).

---

## 3. Six Core Azure Service Categories

### Compute
Services that provide processing power to run applications and workloads.
- **Virtual Machines (VMs)** — Full virtual computers in the cloud you can configure and control
- **Azure App Service** — A managed platform to deploy and host web apps and APIs without managing the underlying server

### Storage
Services to store data in the cloud reliably and at scale.
- **Azure Blob Storage** — Object storage for unstructured data like images, videos, and backups
- **Azure Disk Storage** — Persistent disk drives attached to virtual machines, like a hard drive in the cloud

### Networking
Services that connect resources together and to the internet securely.
- **Azure Virtual Network (VNet)** — A private network in Azure where your resources communicate securely
- **Azure Load Balancer** — Distributes incoming traffic across multiple servers so no single server gets overloaded

### Identity
Services to manage who users are and what they can access.
- **Microsoft Entra ID (formerly Azure Active Directory)** — Manages user identities, authentication, and access across Azure and Microsoft services
- **Role-Based Access Control (RBAC)** — Assigns permissions to users based on their role (e.g., Admin, Contributor, Reader)

### Monitoring
Services to observe the health and performance of your resources.
- **Azure Monitor** — Collects metrics and logs from all Azure resources to give visibility into what is happening
- **Log Analytics** — A tool within Azure Monitor that lets you query and analyze logs from your resources

### Security
Services to protect your cloud resources and data.
- **Microsoft Defender for Cloud** — Continuously assesses your environment for security vulnerabilities and threats
- **Azure Key Vault** — Securely stores secrets, passwords, API keys, and certificates so applications never store sensitive data in code

---

## 4. Azure Pricing

### Consumption Model (Pay-As-You-Go)
Azure charges you only for what you actually use. If you run a VM for 3 hours, you pay for 3 hours. If you turn it off, you stop paying. There are no upfront costs or long-term commitments required — this makes cloud much more cost-effective than buying physical hardware.

### Free Tier
Azure offers two types of free resources:
- **Always free** — Some services are free forever with usage limits (e.g., Azure Functions up to 1 million requests/month)
- **12-month free** — Popular services like VMs and Blob Storage are free for the first 12 months for new accounts, within set limits
- **$200 credit** — New Azure accounts receive a $200 credit for the first 30 days to explore any services

### SLA (Service Level Agreement)
An SLA is Microsoft's promise about how much uptime a service will have. It is expressed as a percentage.

| SLA % | Downtime per Year | Downtime per Month |
|---|---|---|
| 99% | ~87.6 hours | ~7.3 hours |
| 99.9% | ~8.7 hours | ~43.8 minutes |
| 99.95% | ~4.4 hours | ~21.9 minutes |
| 99.99% | ~52.6 minutes | ~4.4 minutes |

For example, a 99.9% SLA means your service could be unavailable for up to **43 minutes per month** — and Microsoft will compensate you if they exceed that downtime.

---

## 5. Entra ID Basics

**Microsoft Entra ID** is Azure's identity and access management service. It is the system that controls who can log in and what they are allowed to do across Azure and Microsoft services.

**Users** are individual accounts representing a person or application, each with their own credentials (username and password). **Groups** are collections of users — for example, all developers in one group and all managers in another — which makes it easy to assign permissions to many people at once. **Multi-Factor Authentication (MFA)** adds an extra layer of security by requiring users to verify their identity using a second method beyond just a password, such as a fingerprint, a phone notification, or a one-time code. **Role-Based Access Control (RBAC)** is the system that assigns specific permissions based on a user's role — for example, an Admin can create and delete resources, a Contributor can manage resources but not control access, and a Reader can only view resources without making any changes.

---

## 6. Governance

### Azure Policy
Azure Policy is a set of rules that enforces standards and compliance across your Azure environment. For example, you can create a policy that says "no resources can be created outside the UK region" or "all VMs must use a specific size." If someone tries to create a resource that violates the policy, Azure will block or flag it automatically.

### Resource Locks
A resource lock prevents resources from being accidentally **deleted or modified**. For example, if you have a critical production database, you can apply a lock so that even if someone with admin permissions tries to delete it, Azure will block the action. There are two types: **Delete lock** (prevents deletion but allows changes) and **Read-only lock** (prevents both deletion and modification).

### Cost Management
Azure Cost Management is a tool that helps you monitor, analyze, and control your cloud spending. It shows you a breakdown of how much each resource, resource group, or subscription is costing you, helps you set budgets and alerts when spending reaches a threshold, and gives you reports to identify where money is being wasted — such as resources left running when they are no longer needed.

---

