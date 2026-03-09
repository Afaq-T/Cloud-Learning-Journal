# AZ-900 Azure Fundamentals Notes 

---

## WEEK 3 — MONDAY NOTES
### Topic: What is Cloud Computing + How Azure is Organized

---

## 1. WHAT IS CLOUD COMPUTING?

Cloud computing means **using someone else's computers over the internet** instead of buying your own.

**Simple Real Example:**  
Instead of buying a ₹200,000 server for your office and maintaining it yourself, you just rent computing power from Microsoft Azure and pay only for what you use — like paying for electricity instead of buying a generator.

**Key Benefits:**
- No upfront hardware cost
- Pay only for what you use (like a mobile data plan)
- Scale up or down anytime (busy season? add more power. Quiet season? reduce it)
- Access from anywhere in the world

---

## 2. THREE SERVICE MODELS (IaaS, PaaS, SaaS)

Think of it like ordering food:

| Model | What You Get | Real Example | You Manage | Azure Manages |
|-------|-------------|--------------|------------|---------------|
| **IaaS** | Raw ingredients | Azure Virtual Machines | OS, Apps, Data | Hardware, Network |
| **PaaS** | Semi-cooked meal kit | Azure App Service | Your App + Data | OS, Runtime, Hardware |
| **SaaS** | Restaurant meal, fully cooked | Microsoft 365, Gmail | Just your data | Everything else |

---

### IaaS — Infrastructure as a Service
- You rent a **virtual machine** (like renting a computer in a data center)
- You install the operating system, install software, manage security yourself
- **Real Example:** You rent an Azure VM, install Ubuntu on it, then install your Python web app
- **Best for:** Companies that want full control, or migrating old apps to cloud

---

### PaaS — Platform as a Service
- You just upload your **code/application** and Azure runs it
- You don't worry about servers, OS updates, or networking
- **Real Example:** You build a website in Python/Node.js and deploy it to Azure App Service. You never touch a server.
- **Best for:** Developers who want to focus on coding, not infrastructure

---

### SaaS — Software as a Service
- You just **open and use** the application — nothing to install or manage
- **Real Example:** Microsoft 365 (Word, Excel online), Gmail, WhatsApp Web
- **Best for:** End users, business teams, everyday work tools

---

### Shared Responsibility Model (Important for Exam!)
The more managed the service, the more Microsoft handles:

```
On-Premises  →  IaaS  →  PaaS  →  SaaS
You manage everything        Microsoft manages everything
```

**You always own:** Your data and who has access to it (in all 3 models)

---

## 3. CLOUD DEPLOYMENT TYPES

| Type | Meaning | Example |
|------|---------|---------|
| **Public Cloud** | Everything on Azure's servers, shared infrastructure | Your startup app on Azure |
| **Private Cloud** | Cloud just for your company, your own data center | A bank running its own private cloud |
| **Hybrid Cloud** | Mix of both | Company keeps sensitive data on-premise, puts website on Azure |

---

## 4. HOW AZURE IS ORGANIZED

Think of it like a company structure:

```
TENANT (Your company's identity — like your company name)
  └── SUBSCRIPTION (Billing account — like a department budget)
        └── RESOURCE GROUP (A folder — like a project folder)
              └── RESOURCES (The actual things — VMs, databases, storage)
```

**Real Example:**  
- **Tenant:** Gordon College (the whole organization in Azure)
- **Subscription:** IT Department Budget (pays the bills)
- **Resource Group:** "Student-Portal-Project" (groups related things)
- **Resources:** 1 VM + 1 Database + 1 Storage Account (actual stuff inside)

---

### Tenant
- Your organization's identity in **Entra ID** (formerly Azure Active Directory)
- Like your company's account with Microsoft
- All users, all subscriptions belong to a single tenant

---

### Subscription
- A **billing container** — everything inside gets billed to it
- One tenant can have multiple subscriptions
- **Real Example:** One subscription for Development, one for Production, one for Testing

---

### Resource Group
- A **logical folder** to organize related resources
- Resources in a group usually belong to the same project or application
- You can delete a whole resource group and it deletes everything inside
- **Real Example:** Resource Group "MyWebApp-RG" contains: 1 Web Server VM + 1 SQL Database + 1 Storage Account

---

### Resources
- The actual things you create in Azure
- Examples: Virtual Machine, Storage Account, SQL Database, Virtual Network
- Every resource must live inside a Resource Group

---

## 5. AZURE REGIONS AND AVAILABILITY ZONES

### Regions
- Azure has **data centers all around the world**, grouped into regions
- **Examples:** East US, West Europe, Southeast Asia, Central India
- You choose which region to deploy your app in
- **Rule:** Choose the region closest to your users for fast performance
- **Real Example:** If your users are in Pakistan, deploy in Central India or UAE North region

---

### Availability Zones
- Each region has **multiple separate data centers** called Availability Zones (AZ)
- They are physically separate buildings with their own power, cooling, networking
- If one zone goes down (fire, flood), others keep running
- **Real Example:** Your app runs in Zone 1. Zone 1's power fails. Azure automatically serves from Zone 2. Users notice nothing.
- **Why it matters:** High availability = your app stays online even if hardware fails

---

### Region Pairs
- Azure pairs regions together for disaster recovery
- **Example:** East US is paired with West US
- If a huge disaster hits East US, Azure fails over to West US automatically

---

## 6. FIVE CORE AZURE SERVICES (Must Know!)

### 1. Virtual Machines (VM) — IaaS Compute
- A computer running in Azure's data center that you fully control
- You choose: Windows or Linux, size (CPU/RAM), storage
- **Real Example:** You create a Windows VM, remote desktop into it, install your software
- **Use when:** You need full control of the OS, running legacy applications

---

### 2. App Service — PaaS for Web Apps
- Deploy your web application without managing any servers
- Supports: Python, Node.js, PHP, Java, .NET, Ruby
- Azure handles scaling, patching, load balancing automatically
- **Real Example:** You push your Django/Flask Python app to App Service. Done. It's live.
- **Use when:** Building websites, REST APIs, mobile backends

---

### 3. Blob Storage — File Storage in the Cloud
- Store any file: images, videos, PDFs, backups, logs
- "Blob" = Binary Large Object (just means any type of file)
- Extremely cheap and can store unlimited amount of data
- **Real Example:** Your app lets users upload profile pictures → store them in Blob Storage
- **Use when:** Storing files, backups, static website content, big data

---

### 4. VNet (Virtual Network) — Azure Networking
- A private network inside Azure, just like your home/office WiFi network
- Your VMs, databases etc. connect through VNet to talk to each other securely
- Controls which resources can communicate with each other
- **Real Example:** Your web server VM talks to your database VM through a VNet. Database is never exposed to the internet.
- **Use when:** Any time you need private, secure communication between Azure resources

---

### 5. Entra ID (formerly Azure Active Directory) — Identity and Access
- Microsoft's cloud-based identity system
- Manages **who can log in** and **what they can access**
- **Real Example:** When you log into Microsoft Teams or Office 365 with your work email → that's Entra ID authenticating you
- **Use when:** Managing users, groups, login security, multi-factor authentication (MFA)

---

## 7. QUICK SUMMARY TABLE

| Concept | Simple Explanation | Real Example |
|---------|-------------------|-------------|
| Cloud Computing | Renting computers over internet | Using Azure instead of buying servers |
| IaaS | Rent a virtual machine, you manage it | Azure Virtual Machines |
| PaaS | Deploy your app, Azure manages the rest | Azure App Service |
| SaaS | Use a ready-made app | Microsoft 365, Gmail |
| Tenant | Your organization's Azure identity | Gordon College's Azure account |
| Subscription | Billing container | IT Department's budget account |
| Resource Group | Project folder | "StudentPortal-RG" |
| Resource | Actual thing you create | VM, Database, Storage |
| Region | Location of Azure data centers | East US, Central India |
| Availability Zone | Separate buildings in same region | Zone 1, Zone 2, Zone 3 |
| Virtual Machine | Rented computer in Azure | Windows Server VM |
| App Service | Host web apps without servers | Deploy Django app |
| Blob Storage | File storage | Store user profile photos |
| VNet | Private network in Azure | Connect VM to Database privately |
| Entra ID | Login and identity management | Work login for Office 365 |

---

## 8. EXAM TIPS (AZ-900)

- IaaS = **most control**, you manage OS and up
- SaaS = **least control**, Microsoft manages everything
- You **always** own your data regardless of model
- Availability Zones = protection against **data center failure**
- Region Pairs = protection against **regional disaster**
- Resource Groups = logical containers, NOT physical location
- Entra ID is NOT the same as on-premises Active Directory (it's cloud-based)

---

## Key Analogies To Remember

- CapEx vs OpEx = Buying a car vs Uber
- SLA: 99.9% = 43min, 99.95% = 21min, 99.99% = 4min downtime/month
- Policy = Security guard (blocks), RBAC = Key card (who), Advisor = Consultant (suggests)
- Reserved = Bus pass, Pay-As-You-Go = Taxi, Spot = Standby flight

## MY RESOURCES
- 📺 John Savill Full Course: https://youtube.com/playlist?list=PLlVtbbG169nED0_vMEniWBQjSoxTsBYS3
- ⚡ Study Cram (watch before exam): https://youtu.be/tQp1YkB2Tgs
- 📖 Free Handout PDF: https://github.com/johnthebrit/AZ900CertCourse
- 🖥️ Microsoft Learn Labs: https://learn.microsoft.com/training/paths/microsoft-azure-fundamentals-describe-cloud-concepts/

---

