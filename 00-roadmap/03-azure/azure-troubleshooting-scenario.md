# Azure Troubleshooting Scenarios — Week 3

---

## Scenario 1: A Resource Deployment is Failing

**Problem:** A user is trying to deploy a new resource in Azure but the deployment keeps failing.

**What I would check in order:**

1. Check the **Activity Log** in the Azure portal — go to the subscription, click Activity Log, find the failed deployment and read the exact error message. This tells you the real reason immediately.
2. Check if the **resource name is already taken** — storage accounts and some other resources require globally unique names across all of Azure. If the name exists anywhere in the world, deployment fails.
3. Check if the **selected region supports** that resource type — not all services are available in all regions.
4. Check if the **subscription has hit its quota limit** — every subscription has limits on how many VMs, cores, and other resources you can create.
5. Check if the **user has the correct permissions** — they need at least Contributor role on the Resource Group to deploy resources.
6. Check if the **Resource Group exists** — you cannot deploy into a Resource Group that has not been created yet.

**Resolution:** Fix the specific issue found in the Activity Log error message. Most common fix is renaming the resource or assigning the correct RBAC role to the user.

**Escalate when:** The error message is unclear, quota increase is needed (requires Microsoft support ticket), or the issue affects the entire subscription.

---

## Scenario 2: User Cannot Access a Specific Resource

**Problem:** A user can see the Azure portal but when they try to open a specific resource it says Access Denied.

**What I would check in order:**

1. Go to the resource and click **Access Control (IAM)** then **Role Assignments** tab — check if the user has any role assigned directly or through a group.
2. Check the **scope of the role** — the role might be assigned to a different Resource Group or Subscription, not the one containing this resource.
3. Check if the user is in the correct **Entra ID group** — permissions are often assigned to groups, not individual users.
4. Check for **Deny assignments** — a Deny assignment always overrides an Allow assignment regardless of role. Even if the user has Contributor, a Deny assignment blocks them.
5. Check if the user is signed in with the **correct account** — some users have both personal and work Microsoft accounts.

**Resolution:** Assign the correct RBAC role (Reader, Contributor, or Owner) at the correct scope to the user or their group. Remove any incorrect Deny assignments.

**Escalate when:** The role assignment looks correct but access is still denied — this may require checking Conditional Access policies or Entra ID group membership at admin level.

---

## Scenario 3: Azure Bill is Unexpectedly High

**Problem:** The Azure bill this month is 3x higher than normal and nobody deployed anything new.

**What I would investigate in order:**

1. Go to **Cost Management and Billing** in the portal — look at the cost breakdown by resource type and identify which service is causing the spike.
2. Check for **VMs that are running but not being used** — in Azure, a VM that is running charges you even if no one is using it. A VM must be Deallocated (not just Stopped) to stop compute charges.
3. Check **storage tiers** — if data was moved from Cool or Archive tier to Hot tier, costs increase significantly.
4. Check if any **premium tier service** was accidentally used instead of standard tier.
5. Open **Azure Advisor** and click the Cost tab — it shows specific recommendations for reducing spend on your account.
6. Check **resource tags** — if tags are not set correctly, costs cannot be attributed to the right project or team making it hard to find the source.

**Resolution:** Deallocate unused VMs, move storage to cheaper tiers, delete unused resources. Set up budget alerts in Cost Management so this is caught earlier next time.

**Escalate when:** The cost spike is very large and you cannot identify the source, or it appears resources were created by an unauthorized user — this could indicate a security breach.

---

## Scenario 4: Cannot RDP into an Azure Windows VM

**Problem:** A user says they cannot RDP into their Azure Windows VM.

**What I would check in order:**

1. **Is the VM in Running state?** Go to the VM in the portal and check the status. If it shows Stopped or Deallocated, start it. A VM that is not running cannot be reached by anything.
2. **Does the VM have a Public IP address?** Go to the VM overview page and check the Public IP field. If it is blank or None, the VM cannot be reached from outside Azure. You must attach a Public IP to the VM's network interface.
3. **Are NSG rules allowing port 3389?** Click Networking on the VM's left menu. Check both the subnet-level NSG and the NIC-level NSG. Look for an inbound rule allowing TCP port 3389. If no such rule exists, RDP is blocked at network level. Add the rule.
4. **Is the Windows Firewall inside the VM blocking RDP?** Even if Azure NSGs allow port 3389, the Windows Firewall inside the operating system might block it. Check this through Boot Diagnostics or Azure Serial Console.
5. **Are the credentials correct?** Check the username and password. If the password is forgotten, use the Reset Password option in the VM's Support and Troubleshooting section in the portal.

**Resolution:** Fix whichever step above is failing. Most common cause is either the VM not running or NSG missing the port 3389 allow rule.

**Escalate when:** VM is running, NSG rules are correct, but still cannot connect — may require deeper OS-level investigation or Azure support.

---

## Scenario 5: Website on Azure App Service Not Loading

**Problem:** A company's website was working yesterday but today it is not loading for anyone.

**What I would check in order:**

1. **Is the App Service in Running state?** Go to the App Service in the portal and check the status at the top. If it shows Stopped, start it.
2. **Check Deployment Center** — go to the App Service, click Deployment Center in the left menu, and look at the deployment history. If the most recent deployment failed, the app may be in a broken state. Roll back to the previous working deployment.
3. **Check Log Stream** — go to Monitoring then Log Stream in the App Service menu. This shows real-time application errors. Look for any error messages that explain why the app is failing.
4. **Check the App Service Plan** — if the plan is on Free or Basic tier it may have run out of CPU or memory quota. Go to the App Service Plan and check the metrics.
5. **Check subscription status** — if the subscription has expired or hit a spending limit, all resources including App Service stop working.

**Resolution:** Restart the App Service, roll back a bad deployment, or scale up the App Service Plan if resources are exhausted.

**Escalate when:** Logs show errors in the application code itself — this requires the development team, not the support engineer.

---

## Key Terms Reference

| Term | Meaning |
|---|---|
| RDP | Remote Desktop Protocol — used to remotely control a Windows VM, runs on port 3389 |
| NSG | Network Security Group — Azure firewall that allows or denies traffic based on rules |
| RBAC | Role Based Access Control — controls who can do what in Azure using roles and scopes |
| Activity Log | Record of all operations in Azure — first place to check when deployment fails |
| Entra ID | Microsoft's identity service — manages users, groups, and access |
| Deallocated | VM is fully stopped and not being charged for compute |
