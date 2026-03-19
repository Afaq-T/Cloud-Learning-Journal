# RBAC Cheatsheet

## The 4 Built-in Roles

| Role | What it CAN do | What it CANNOT do |
|---|---|---|
| **Owner** | Full access to all resources + manage role assignments | Nothing restricted |
| **Contributor** | Create, modify, and delete all resources | Cannot manage access for others |
| **Reader** | View all resources and settings | Cannot create, modify, delete, or manage access |
| **User Access Administrator** | Manage role assignments only | Cannot touch any resources |

### One-sentence description of each role

**Owner** — Full control including the ability to give or remove access for other users.

**Contributor** — Can do everything with resources except control who has access to them.

**Reader** — View-only access, cannot change anything.

**User Access Administrator** — Can manage access for others but cannot create or touch any resources.

---

## Scope Hierarchy — Permissions Inherit Downward

```
Management Group
        │
        ▼
  Subscription
        │
        ▼
  Resource Group
        │
        ▼
    Resource
```

### How inheritance works
- A role assigned at **Subscription** level applies to ALL resource groups and resources inside it
- A role assigned at **Resource Group** level applies to ALL resources inside that group only
- A role assigned at **Resource** level applies to ONLY that specific resource
- Permissions flow DOWN — never up

### Example
If you assign Reader at Subscription level:
- User can view ALL resource groups in that subscription ✅
- User can view ALL resources in ALL resource groups ✅
- User cannot view other subscriptions ❌

If you assign Contributor at Resource Group A:
- User can manage resources inside Resource Group A ✅
- User cannot touch Resource Group B ❌
- User cannot manage access for others in Resource Group A ❌

---

## Deny Assignments — The Override Rule

> **DENY ALWAYS OVERRIDES ALLOW — no exceptions**

Even if a user has Owner role at Subscription level, a single Deny assignment on a specific resource blocks all access to that resource.

**How to check for Deny assignments:**
1. Go to the resource in Azure portal
2. Click **Access Control (IAM)**
3. Click **Deny assignments** tab

---

## 5 Most Common RBAC Mistakes

### Mistake 1 — Giving Owner when Contributor is enough
User gets access to manage role assignments they should not have.
Fix: Always assign the minimum role needed.

### Mistake 2 — Assigning roles to individuals instead of groups
Hard to manage at scale. When someone leaves, their individual assignment is often forgotten.
Fix: Always assign roles to Entra ID groups. Add/remove users from the group only.

### Mistake 3 — Forgetting that Deny overrides Allow
User has Contributor on subscription but still gets Access Denied on a specific resource.
Fix: Always check the Deny assignments tab first when access is denied despite having a role.

### Mistake 4 — Not reviewing role assignments — access accumulates
Users change departments but old access is never removed — a major security risk.
Fix: Use Entra ID Access Reviews to automatically audit who has what access quarterly.

### Mistake 5 — Confusing Azure RBAC with Entra ID roles
Azure RBAC controls Azure resources. Entra ID roles control Entra ID itself. These are completely separate systems.
Fix: Use Azure RBAC for resource access. Use Entra ID roles for directory management.

---

## Quick Reference — When to Use Which Role

| Scenario | Correct Role |
|---|---|
| New junior employee — view resources only | Reader |
| Developer needs to deploy apps | Contributor |
| Manager needs full control of a resource group | Owner (scoped to that resource group only) |
| IT admin needs to assign roles to others | User Access Administrator |
| Auditor needs to check configurations | Reader |
| DevOps engineer needs to create and delete resources | Contributor |

---

## Principle of Least Privilege

> Always assign the **minimum access** needed to do the job — nothing more.

1. Start with Reader for everyone
2. Only elevate to Contributor when someone needs to create/manage resources
3. Only give Owner when someone needs to manage access for others
4. Review and reduce access whenever someone changes roles

---

## How to Create an RBAC Assignment

1. Go to **portal.azure.com**
2. Navigate to the resource, resource group, or subscription
3. Click **Access Control (IAM)** → **Add** → **Add role assignment**
4. Select the role → click Next
5. Select members (user or group) → click Next
6. Click **Review + assign** → confirm
7. Verify in Role Assignments tab

---

## Summary — Scope vs Role Matrix

| | Owner | Contributor | Reader | User Access Admin |
|---|---|---|---|---|
| **View resources** | ✅ | ✅ | ✅ | ✅ |
| **Create resources** | ✅ | ✅ | ❌ | ❌ |
| **Delete resources** | ✅ | ✅ | ❌ | ❌ |
| **Assign roles** | ✅ | ❌ | ❌ | ✅ |
| **Remove roles** | ✅ | ❌ | ❌ | ✅ |
