# Week 3 Quiz — Azure Fundamentals (AZ-900 Level)
**Total Questions: 30 | Topics: Cloud Concepts, Azure Services, Governance, Identity, Pricing, Networking**

---

## Round 1 — Cloud Basics

**Q1. What does IaaS stand for and what is an example?**
- A) Internet as a Service — Gmail
- B) Infrastructure as a Service — Virtual Machines ✅
- C) Integration as a Service — Microsoft 365
- D) Infrastructure as a Software — App Service

**Answer: B**
IaaS means Infrastructure as a Service. The cloud provider gives you virtual machines and networking infrastructure. You manage the operating system and applications yourself. Example: Azure Virtual Machines.

---

**Q2. Which service model does Microsoft 365 fall under?**
- A) IaaS
- B) PaaS
- C) SaaS ✅
- D) None

**Answer: C**
Microsoft 365 is Software as a Service. The provider manages everything — infrastructure, platform, and the software itself. You just use it through a browser or app.

---

**Q3. In Azure hierarchy, what sits directly ABOVE a Resource Group?**
- A) Tenant
- B) Resource
- C) Subscription ✅
- D) Management Group

**Answer: C**
The Azure hierarchy from top to bottom is: Tenant → Subscription → Resource Group → Resource. Subscription sits directly above Resource Group and is the billing container.

---

**Q4. What does SLA stand for?**
- A) Server Level Access
- B) Service Level Agreement ✅
- C) System Login Authentication
- D) Software License Agreement

**Answer: B**
SLA stands for Service Level Agreement. It is Microsoft's guarantee of uptime for a service. If they fail to meet it, they provide service credits.

---

**Q5. Azure's 99.9% SLA means approximately how much downtime per MONTH?**
- A) 8.7 hours
- B) 1 hour
- C) 43 minutes ✅
- D) 10 minutes

**Answer: C**
99.9% SLA = 0.1% downtime allowed. Per month that equals approximately 43 minutes. Per year that equals approximately 8.7 hours. Always know both figures for interviews.

---

## Round 2 — Azure Services

**Q6. Which Azure service is used for storing files and objects like images and videos?**
- A) Azure VM
- B) Azure Blob Storage ✅
- C) Azure VNet
- D) Azure App Service

**Answer: B**
Blob Storage is Azure's object storage service. It stores unstructured data like images, videos, backups, and log files. It falls under the Storage service category.

---

**Q7. What is Azure Entra ID used for?**
- A) Storing data
- B) Managing virtual networks
- C) Identity and access management ✅
- D) Monitoring resources

**Answer: C**
Entra ID (formerly Azure Active Directory) is Microsoft's cloud identity service. It manages users, groups, authentication, and access control for Azure and Microsoft 365.

---

**Q8. Which Azure service is PaaS for hosting web applications?**
- A) Virtual Machine
- B) Blob Storage
- C) App Service ✅
- D) VNet

**Answer: C**
App Service is a PaaS offering. You deploy your application code and Microsoft manages the underlying infrastructure, OS, and runtime. You focus only on your app.

---

**Q9. What are two services under Azure Networking?**
- A) VNet and Blob Storage
- B) VNet and Load Balancer ✅
- C) Entra ID and VNet
- D) App Service and NSG

**Answer: B**
Azure Networking services include VNet (Virtual Network), Load Balancer, NSG (Network Security Group), VPN Gateway, and Azure DNS. VNet and Load Balancer are core networking services.

---

**Q10. Azure Monitor belongs to which service category?**
- A) Security
- B) Compute
- C) Identity
- D) Monitoring ✅

**Answer: D**
Azure Monitor is the core monitoring service in Azure. It collects metrics and logs from all resources, sets alerts, and integrates with Log Analytics for deeper analysis.

---

## Round 3 — Governance & Security

**Q11. What is a Resource Lock used for?**
- A) Saving costs by stopping resources
- B) Preventing accidental deletion or modification of resources ✅
- C) Locking user accounts
- D) Blocking internet access to a resource

**Answer: B**
Resource Locks protect important resources from accidental deletion or modification. There are two types: ReadOnly (no changes allowed) and Delete (cannot be deleted but can be modified).

---

**Q12. What does Azure Policy do?**
- A) Monitors CPU usage
- B) Manages user passwords
- C) Enforces rules and standards on Azure resources ✅
- D) Controls network traffic

**Answer: C**
Azure Policy enforces organizational rules across your Azure environment. Example: a policy that says all resources must have a specific tag, or all VMs must be deployed only in certain regions.

---

**Q13. What is RBAC?**
- A) Resource Based Access Control
- B) Role Based Access Control ✅
- C) Remote Backup Access Control
- D) Regional Billing Access Control

**Answer: B**
RBAC stands for Role Based Access Control. It controls who can do what in Azure by assigning roles (like Reader, Contributor, Owner) to users or groups at a specific scope.

---

**Q14. Which RBAC role can view resources but NOT make any changes?**
- A) Owner
- B) Contributor
- C) Reader ✅
- D) Administrator

**Answer: C**
Reader role allows viewing all resources but cannot create, modify, or delete anything. It is the minimum access role and follows the principle of least privilege.

---

**Q15. What is Cost Management in Azure used for?**
- A) Creating virtual machines
- B) Managing user identities
- C) Tracking and analyzing spending on Azure resources ✅
- D) Setting up virtual networks

**Answer: C**
Cost Management helps you monitor, allocate, and optimize your Azure spending. You can see cost breakdowns by resource, set budgets, and create alerts when spending exceeds a threshold.

---

## Round 4 — MFA & Entra ID

**Q16. What does MFA stand for?**
- A) Multiple Factor Authorization
- B) Multi Factor Authentication ✅
- C) Managed Factor Access
- D) Microsoft Factor Authentication

**Answer: B**
MFA stands for Multi Factor Authentication. It requires users to verify their identity using two or more factors before gaining access to a system.

---

**Q17. Which of these is an example of MFA?**
- A) Username only
- B) Password only
- C) Password + fingerprint ✅
- D) Email only

**Answer: C**
Password + fingerprint combines two factors: something you know (password) and something you are (biometric). This is a strong MFA combination used in modern organizations.

---

**Q18. In Entra ID, what is a GROUP used for?**
- A) Storing files together
- B) Organizing users and assigning permissions collectively ✅
- C) Monitoring resources
- D) Creating virtual networks

**Answer: B**
Groups in Entra ID collect users together so you can assign permissions to the group instead of individual users. When a new employee joins, add them to the group and they inherit all permissions automatically.

---

**Q19. Which MFA factor is "something you ARE"?**
- A) Password
- B) SMS code
- C) Fingerprint or biometric ✅
- D) PIN number

**Answer: C**
The three MFA factor types are: something you KNOW (password, PIN), something you HAVE (phone, SMS code), and something you ARE (fingerprint, face scan, biometric).

---

**Q20. What is the OWNER role in Azure RBAC?**
- A) Can only view resources
- B) Can create resources but not manage access
- C) Has full access including managing other users access ✅
- D) Can only manage user identities

**Answer: C**
Owner has full control over all resources AND can manage who has access (role assignments). It is the highest privilege role. Always assign Owner sparingly — use Contributor when full access is not needed.

---

## Round 5 — Azure Pricing & Regions

**Q21. What does the Azure consumption model mean?**
- A) Pay a fixed monthly fee regardless of usage
- B) Pay only for what you use ✅
- C) Pay upfront for one year
- D) Free forever

**Answer: B**
The consumption model (pay-as-you-go) means you are charged only for the resources you actually use. If you stop a VM, you stop paying for compute. This is the default Azure pricing model.

---

**Q22. What is an Availability Zone in Azure?**
- A) A country where Azure operates
- B) A separate physical data center within the same region ✅
- C) A group of subscriptions
- D) A type of virtual machine

**Answer: B**
Availability Zones are physically separate data centers within the same Azure region. They have independent power, cooling, and networking. Deploying across zones protects against single data center failures.

---

**Q23. Which of these is a real Azure Region?**
- A) North Pakistan
- B) East US ✅
- C) Central Moon
- D) West China Sea

**Answer: B**
Real Azure regions include East US, West US, West Europe, North Europe, Southeast Asia, and many more. Azure has over 60 regions worldwide. Memorize at least 5 common ones for interviews.

---

**Q24. What is Azure Free Tier?**
- A) Pay as you go model
- B) Some services free for 12 months or always free with limits ✅
- C) Free only for students
- D) Free only for enterprises

**Answer: B**
Azure Free Tier includes: always-free services (like 5GB Blob Storage), services free for 12 months (like 750 hours of B1S VM), and a $200 credit for the first 30 days for new accounts.

---

**Q25. Why do Availability Zones matter?**
- A) They reduce the cost of resources
- B) They provide redundancy if one data center fails ✅
- C) They speed up internet connection
- D) They store backup passwords

**Answer: B**
Availability Zones provide high availability and redundancy. If one zone goes down due to power failure or disaster, your resources in other zones keep running without interruption.

---

## Round 6 — Mixed Hard Questions

**Q26. Which Azure service category does Defender for Cloud belong to?**
- A) Monitoring
- B) Compute
- C) Security ✅
- D) Identity

**Answer: C**
Defender for Cloud is a security posture management tool. It monitors your Azure resources for security vulnerabilities and provides recommendations. It belongs to the Security category along with Key Vault.

---

**Q27. What is a Tenant in Azure?**
- A) A billing container for resources
- B) The organization's identity at the top of Azure hierarchy ✅
- C) A group of virtual machines
- D) A type of storage account

**Answer: B**
A Tenant represents your organization in Azure and Entra ID. It is the top level of the hierarchy. Every organization that uses Azure or Microsoft 365 has exactly one Tenant. It contains all your users, groups, and subscriptions.

---

**Q28. A user can delete resources but should only view them. What do you do?**
- A) Delete their account
- B) Remove Contributor role and assign Reader role ✅
- C) Add Owner role
- D) Create a new resource group

**Answer: B**
If a user has Contributor they can create, modify, and delete resources. To restrict them to view only, remove the Contributor role assignment and assign the Reader role instead at the correct scope.

---

**Q29. Which service monitors all Azure resources and sends alerts?**
- A) Azure Policy
- B) Azure Defender
- C) Azure Monitor ✅
- D) Cost Management

**Answer: C**
Azure Monitor collects metrics and logs from all Azure resources, creates dashboards, and fires alerts when thresholds are breached (like CPU above 90% for 15 minutes). It integrates with Log Analytics for advanced queries.

---

**Q30. What happens when a Deny rule and Allow rule conflict in an NSG?**
- A) Allow rule wins
- B) The latest rule wins
- C) Deny rule always wins ✅
- D) Both rules are ignored

**Answer: C**
In Azure NSGs, a Deny assignment ALWAYS overrides an Allow assignment regardless of priority number. This is a critical rule to remember — if you cannot access a resource despite having a role, check for Deny assignments first.

---

## My Week 3 Score Summary

| Round | Topic | Score |
|---|---|---|
| Round 1 | Cloud Basics | 4/5 |
| Round 2 | Azure Services | 5/5 |
| Round 3 | Governance & Security | 5/5 |
| Round 4 | MFA & Entra ID | 5/5 |
| Round 5 | Pricing & Regions | 4/5 |
| Round 6 | Mixed Hard | 4/5 |
| **Total** | | **27/30 — 90%** |

## Areas to Review Before AZ-900 Exam
- IaaS = Infrastructure (not Internet) — example is Virtual Machines
- Azure Regions — memorize: East US, West Europe, Southeast Asia, North Europe
- Deny rule ALWAYS overrides Allow rule in NSGs and RBAC
