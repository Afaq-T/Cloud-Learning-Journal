# Entra ID & Identity Management Notes — Week 4 Monday
---

## Module 1: What is Microsoft Entra ID?

### Key Concepts
- Microsoft Entra ID (formerly Azure Active Directory) is Microsoft's cloud identity and access management service
- Every organization using Azure, Microsoft 365, or Teams runs on Entra ID
- It manages users, groups, authentication, and access control
- It sits at the top of the Azure hierarchy inside the Tenant

### Explain to a Friend
Entra ID is like the security desk at the entrance of a large office building. It checks who you are (authentication), decides which floors and rooms you can access (RBAC), and makes sure you prove your identity with more than just a key card (MFA). Every employee has a record at this security desk.

### Exam Question
**Q: What is Microsoft Entra ID used for?**
A: It is Microsoft's cloud identity and access management service that manages users, groups, authentication (MFA, SSO), and access control (RBAC) for Azure and Microsoft 365.

---

## Module 2: Users and Guests

### Key Concepts

**Internal Users**
- Individual accounts created inside your organization's Entra ID tenant
- Every employee gets one user account with their name, email, credentials, and Object ID
- Object ID is a unique identifier that never changes — used to track the user across the system
- When onboarding a new employee: Create user account → Add to appropriate group → Group has role assigned

**Guest Users**
- External users from outside your organization invited into your tenant
- Example: a partner company consultant who needs temporary access to your resources
- Guests have limited permissions by default — they cannot see the full directory
- Guest status shows in Entra ID under External Identities

**Sign-in Logs**
- Entra ID records every sign-in attempt — successful and failed
- Found under: Entra ID → Sign-in Logs
- Shows: username, location, device, time, success/failure, MFA status
- Critical for security investigations

### Explain to a Friend
A user is like a permanent employee badge — internal, full access based on their role. A guest is like a visitor badge — external, limited access, and temporary. Sign-in Logs is like the building's entry/exit logbook that records every time someone tried to enter.

### Exam Question
**Q: What is the difference between a user and a guest in Entra ID?**
A: A user is an internal employee account with standard permissions. A guest is from an external organization, invited into the tenant with limited permissions by default. Guests cannot see the full directory and have restricted access.

---

## Module 3: Groups

### Key Concepts
- Groups are collections of users in Entra ID
- **Best practice: Always assign permissions to groups, never to individual users**
- When a new employee joins → add them to the group → they automatically inherit all group permissions
- When an employee leaves → remove them from the group → all access is immediately revoked
- This scales perfectly — no need to update individual role assignments every time

**Two types of groups:**
- **Security Groups** — used for assigning access to Azure resources (most common)
- **Microsoft 365 Groups** — used for collaboration (Teams, SharePoint, etc.)

**Why groups over individuals:**
- Scales easily for large organizations
- Consistent permissions across teams
- Easier auditing and access reviews
- One change updates everyone in the group

### Explain to a Friend
Think of groups like department keys. Instead of giving every IT employee their own individual key to the server room, you give the "IT Department" key to the IT group. When someone joins IT, you give them the group key. When they leave, you take it back. Much easier than managing individual keys for 50 people.

### Exam Question
**Q: Why should you assign RBAC roles to groups instead of individual users?**
A: Because when someone joins or leaves a team, you only update their group membership and their access updates automatically. This scales efficiently and ensures consistent permissions without manually updating individual role assignments.

---

## Module 4: MFA — Multi Factor Authentication

### Key Concepts
- MFA requires users to verify identity using two or more factors before gaining access
- In 2026 every organization requires MFA — it is non-negotiable for any support engineer

**Three MFA factor types:**

| Factor Type | What it is | Examples |
|---|---|---|
| Something you KNOW | Information only you know | Password, PIN |
| Something you HAVE | Physical device you possess | Phone app, SMS code, hardware token |
| Something you ARE | Your physical characteristics | Fingerprint, face scan, biometric |

**MFA is NOT:**
- Username alone (not a factor — just an identifier)
- MFA does not make accounts 100% unhackable (social engineering still exists)
- MFA does not replace passwords — it adds a second layer on top

**MFA Lockout Recovery:**
When a user cannot sign in because their MFA device is broken or lost:
1. Admin goes to Entra ID → Users → find the user
2. Click Authentication Methods
3. Issue a **Temporary Access Pass (TAP)** — a time-limited one-time code
4. User signs in with TAP and immediately registers new MFA device
5. TAP expires automatically after the set time

**Important:** Never tell a locked-out user to "just reinstall the app" — they cannot log in to do anything. The admin must issue the TAP first.

### Explain to a Friend
MFA is like a bank vault that needs both a key AND a PIN code to open. Even if someone steals your key (password), they still cannot open the vault without the PIN (your phone). Two locks are always better than one.

### Exam Question
**Q: A user's phone broke and they cannot sign in because MFA is required. What does the admin do?**
A: The admin goes to Entra ID, finds the user, clicks Authentication Methods, and issues a Temporary Access Pass — a time-limited code the user can use to sign in once without MFA and then register their new device.

---

## Module 5: SSO — Single Sign-On

### Key Concepts
- SSO means a user logs in once and gets access to all connected applications without logging in separately to each one
- Example: Employee logs into their laptop in the morning → automatically accesses Teams, Outlook, SharePoint, Salesforce, GitHub — all without another login
- Works because all apps are connected to Entra ID as the identity provider

**Benefits for users:**
- No password fatigue — fewer passwords to remember
- Faster access to tools
- Better productivity

**Benefits for organizations:**
- Reduced attack surface — fewer passwords means fewer credential risks
- Centralized access control — revoke SSO and user loses access to everything at once
- Easier compliance and auditing

**SSO vs MFA — they work together:**
- SSO = log in once for convenience
- MFA = make that one login very secure
- Best practice: SSO + MFA together

### Explain to a Friend
SSO is like a master keycard for a hotel. You get one card at check-in and it opens your room, the gym, the pool, and the restaurant — you don't need a separate key for each place. When you check out, the hotel deactivates that one card and you lose access to everything at once.

### Exam Question
**Q: What is Single Sign-On and why do organizations use it?**
A: SSO allows users to log in once and access all connected applications without separate logins. Organizations use it because it reduces password fatigue for users, shrinks the attack surface by having fewer credentials to steal, and allows centralized access control — disabling one account revokes access everywhere.

---

## Module 6: RBAC — Role Based Access Control

### Key Concepts
- RBAC controls who can do what in Azure
- Every RBAC assignment has three parts:
  1. **Role** — what actions are allowed
  2. **Scope** — where the role applies
  3. **Principal** — who gets the access (user, group, or service)

**The 4 Built-in Roles — MEMORIZE THESE:**

| Role | What it can do | What it CANNOT do |
|---|---|---|
| **Owner** | Full access to all resources | Nothing restricted — highest privilege |
| **Contributor** | Create and manage all resources | Cannot manage access for others |
| **Reader** | View all resources | Cannot create, modify, or delete anything |
| **User Access Administrator** | Manage who has access (role assignments) | Cannot touch any resources |

**Scope Hierarchy (permissions inherit downward):**
```
Management Group
    └── Subscription
            └── Resource Group
                    └── Resource
```
A role assigned at Subscription level applies to ALL resource groups and resources inside it.

**Principle of Least Privilege:**
Always assign the minimum access needed. If someone only needs to view resources → Reader. Never give Owner when Contributor is enough.

**DENY always overrides ALLOW:**
- If a user has Contributor at subscription level BUT a Deny assignment on a specific resource → they CANNOT access that resource
- Deny always wins regardless of any Allow assignments at any scope

**5 Most Common RBAC Mistakes:**
1. Giving Owner when Contributor is enough
2. Assigning roles to individuals instead of groups
3. Forgetting that Deny overrides Allow
4. Not reviewing role assignments — people accumulate access over time
5. Confusing Azure RBAC (controls resources) with Entra ID roles (controls Entra ID itself)

### Explain to a Friend
RBAC is like a building access system. The Reader role is like a visitor badge — you can walk around and look but cannot touch anything. Contributor is like a staff badge — you can use all equipment and rooms. Owner is like the master key held by management — full control including giving other people access. And a Deny assignment is like a red "NO ENTRY" sign on a specific room that overrides every badge, even the master key.

### Exam Question
**Q: A developer needs to deploy apps to Azure but must not be able to delete resource groups or manage access for others. Which role do you assign?**
A: Contributor role. It allows creating and managing all resources including deployments, but it cannot delete resource groups at subscription level (only within their assigned scope) and cannot manage role assignments for others.

---

## Module 7: Conditional Access

### Key Concepts
- Conditional Access is how organizations implement Zero Trust in Entra ID
- It creates policies: **IF [condition] THEN [action]**
- Conditions can be: location, device compliance, user risk, sign-in risk, app being accessed
- Actions can be: require MFA, block access, require compliant device

**Common Conditional Access examples:**
- IF sign-in from outside Pakistan → THEN require MFA
- IF device is not enrolled in Intune → THEN block access
- IF sign-in risk is high (leaked credentials) → THEN require password change
- IF location = office network → THEN skip MFA (Named Location trusted)

**Named Locations:**
- Define trusted IP address ranges (like your office network)
- Used in Conditional Access to skip MFA for trusted locations
- Set up: Entra ID → Security → Named Locations

**Identity Protection:**
- Automatically detects risky sign-ins and leaked credentials
- Can force password change when credentials are found on dark web
- Integrates with Conditional Access for automated responses

**CRITICAL — Never disable Conditional Access globally:**
- If a manager is blocked in another country → issue Temporary Access Pass + add their location as trusted
- NEVER turn off Conditional Access for everyone just to fix one person's problem
- Always use exceptions or TAP for individual cases

### Explain to a Friend
Conditional Access is like a smart security guard with a rulebook. Instead of letting everyone in with just a badge, the guard checks extra conditions: "Are you logging in from a strange country? Show me two forms of ID. Is your device company-approved? If not, you cannot enter." The rules adapt to the risk level automatically.

### Exam Question
**Q: A senior manager is travelling to Dubai and Conditional Access is blocking their login. What do you do?**
A: Two steps — First, issue a Temporary Access Pass so they can sign in immediately for their meeting. Second, after the meeting, add UAE as a trusted Named Location or create an exception in the Conditional Access policy for that user. Never disable Conditional Access globally.

---

## Week 4 Monday Summary

| Topic | Understanding Level |
|---|---|
| Entra ID — What it is | ✅ Strong |
| Users vs Guests | ✅ Strong |
| Groups — why assign to groups | ✅ Strong |
| MFA — three factors | ✅ Strong |
| MFA lockout — Temporary Access Pass | ✅ Strong |
| SSO — Single Sign-On | ✅ Strong |
| RBAC — 4 built-in roles | ✅ Strong |
| Principle of least privilege | ✅ Strong |
| Deny overrides Allow | ✅ Strong |
| Conditional Access | ✅ Strong |
| Named Locations | ⚠️ Review |
| Identity Protection | ⚠️ Review |

