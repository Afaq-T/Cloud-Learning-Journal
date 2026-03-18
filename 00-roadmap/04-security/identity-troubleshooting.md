# Identity Troubleshooting Scenarios — Week 4 Wednesday
**Author: Afaq Tahir | Gordon College Rawalpindi | BS Information Technology**
**File location: 04-security/identity-troubleshooting.md**

---

## Scenario 1: User Gets Access Denied on a Resource

### What the user reports
"I am getting Access Denied when trying to open a storage account in Azure. But my manager says I have access."

### My Answer (what I understood)
First I check the role of that person using Role Based Access Control. Then I check if the resource is available. Then I check if there is any Deny assignment overriding their access because Deny always overrides Allow.

### Complete Correct Answer — Step by Step

**Step 1:** Go to the resource (storage account) in the Azure portal and click **Access Control (IAM)** then the **Role Assignments** tab. Look for the user directly — if they are not listed, check if they are in any groups that have role assignments.

**Step 2:** Check the **scope** of the role assignment. The role might be assigned at a different resource group than the one containing this storage account. A role assigned to Resource Group A does not apply to Resource Group B.

**Step 3:** Check for **Deny assignments**. Go to Access Control (IAM) → Deny assignments tab. A Deny assignment always overrides an Allow assignment regardless of role level or scope. Even an Owner role cannot override a Deny.

**Step 4:** Check if the user is signed in with the **correct account**. Some people have both personal and work Microsoft accounts.

**Step 5:** Check if the storage account has its own **access policies** — some storage accounts use Shared Access Signatures or storage-level policies that are separate from RBAC.

### Key Rule to Remember
> Deny ALWAYS overrides Allow — no exceptions, no matter what role the user has.

### Exam Question
**Q: A user has Owner role at subscription level but gets Access Denied on a specific resource. What is the most likely cause?**
A: There is a Deny assignment on that specific resource. Deny assignments always override Allow assignments regardless of the role level or scope.

---

## Scenario 2: User is Locked Out of MFA

### What the user reports
"I bought a new phone and now I cannot sign in. It keeps asking for my authenticator app code but my old phone is broken."

### My Answer (what I understood)
I give them a Temporary Access Pass through Entra ID. This lets them sign in once without MFA so they can register their new phone.

### Complete Correct Answer — Step by Step

**Step 1:** As admin, go to **portal.azure.com** → search **Microsoft Entra ID** → click **Users**.

**Step 2:** Find the affected user and click on their name to open their profile.

**Step 3:** Click **Authentication Methods** in the left menu.

**Step 4:** Click **+ Add authentication method** → select **Temporary Access Pass (TAP)**.

**Step 5:** Set the TAP duration (e.g. 1 hour) and click **Add**. Copy the TAP code and give it to the user securely.

**Step 6:** User signs in using their username + TAP code instead of MFA.

**Step 7:** After signing in with TAP, user immediately goes to **aka.ms/mysecurityinfo** and registers their new phone as an MFA device.

**Step 8:** After registration, TAP expires automatically — user must use new MFA device going forward.

### Critical Mistake to NEVER Make
> Never tell a locked-out user to "just reinstall the authenticator app" — they CANNOT log in to do anything without admin help first. The admin must issue the TAP first.

### Exam Question
**Q: A user's MFA phone is broken and they cannot sign in. What exact steps does the admin take?**
A: Go to Entra ID → Users → find the user → Authentication Methods → issue a Temporary Access Pass with a time limit. Give the code to the user. They sign in with TAP and immediately register their new device at aka.ms/mysecurityinfo.

---

## Scenario 3: User Has Wrong Permissions — Deleting Resources

### What the user reports
Investigation shows a junior developer is accidentally deleting resources. They should only be able to view resources, not modify or delete them.

### My Answer (what I understood)
They currently have Contributor role which allows modifying and deleting resources. I should change it to Reader role. I can also add a Resource Lock on critical resources so nobody can accidentally delete them.

### Complete Correct Answer — Step by Step

**Step 1:** Go to the relevant resource group in Azure portal. Click **Access Control (IAM)** → **Role Assignments** tab.

**Step 2:** Find the developer's name or their group. Note what role they currently have — it is most likely **Contributor** which allows creating, modifying, and deleting resources.

**Step 3:** Click the three dots next to their role assignment → click **Remove**. Confirm removal.

**Step 4:** Click **Add** → **Add role assignment** → select **Reader** role → assign to the user or their group → click **Review and assign**.

**Step 5:** Apply a **Delete Resource Lock** on any critical resources to prevent accidental deletion — even users with Contributor cannot delete a locked resource.

**Step 6:** Verify by checking the Role Assignments tab — confirm Reader is assigned and Contributor is removed.

### Key Rules to Remember
- Contributor = create, modify, delete resources ❌ too much for junior
- Reader = view only, zero changes ✅ correct for junior
- Resource Lock = extra protection even Contributor cannot bypass

### Exam Question
**Q: A developer should only view resources but can currently delete them. What is wrong and how do you fix it?**
A: They have Contributor role when they should have Reader role. Go to Access Control (IAM) on the resource group, remove the Contributor assignment, and add Reader role. Also apply a Delete Resource Lock on critical resources for extra protection.

---

## Scenario 4: Guest User Cannot See Azure Resources

### What the user reports
"I accepted your invitation email but I cannot see any of your Azure resources."

### My Answer (what I understood)
A guest user is an external user from outside the organization. I check their permissions in Entra ID. Then I assign them Reader role through RBAC so they can view the resources they need.

### Complete Correct Answer — Step by Step

**Step 1:** Go to **Entra ID** → click **External Identities** → check the guest user's status. Make sure they properly accepted the invitation — status should show **Accepted** not **Pending**.

**Step 2:** If status is **Pending**, resend the invitation. The guest must accept the invitation email before they can access anything.

**Step 3:** Once status is Accepted, go to the specific resources they need access to. Click **Access Control (IAM)** → **Add role assignment**.

**Step 4:** Select the appropriate role — usually **Reader** for view access. On the Members tab, search for the guest user's email address → select them → click Review and assign.

**Step 5:** Check if any **Conditional Access policies** are blocking external users. Some policies require devices to be enrolled in Intune — a guest's personal device likely is not enrolled. Create an exception if needed.

**Step 6:** Tell the guest user to sign in at **portal.azure.com** using their own organization's credentials (not a new account).

### Key Difference: Guest vs Internal User
| | Internal User | Guest User |
|---|---|---|
| Origin | Your organization | External organization |
| Permissions | Standard based on role | Limited by default |
| Directory visibility | Full | Restricted |
| Invitation needed | No | Yes — must accept |

### Exam Question
**Q: A guest user accepted an invitation but cannot see any resources. What do you check first?**
A: First check External Identities in Entra ID to confirm the invitation status shows Accepted not Pending. Then go to the specific resources and assign an appropriate role (Reader) to the guest user via Access Control (IAM). Also check if Conditional Access policies are blocking external users.

---

## Scenario 5: New Employee Onboarding — Access to 3 Resource Groups

### What the user reports
A new IT team employee joins on Monday and needs immediate access to 3 resource groups.

### My Answer (what I understood)
I assign them Reader role first because new joiners should not have full access. I add them to the correct group which already has access to those 3 resource groups. I do not assign roles directly to the individual because it is hard to manage individually and risky if someone new gets too much access.

### Complete Correct Answer — Step by Step

**Step 1:** Create a **user account** in Entra ID — go to Entra ID → Users → New user. Fill in their name, email, and temporary password.

**Step 2:** Find the **Entra ID group** that represents the IT team (e.g. `grp-it-team`). If it does not exist, create one.

**Step 3:** Add the new employee to the group — go to the group → Members → Add members → search their name → select → save.

**Step 4:** Verify the group already has the correct role assignments on the 3 resource groups. If not, go to each resource group → Access Control (IAM) → Add role assignment → assign the appropriate role to the group.

**Step 5:** The new employee automatically inherits all group permissions immediately — no individual role assignments needed.

**Step 6:** Send them their temporary password and have them sign in and set a permanent password.

### Why NEVER assign roles directly to individual users

| Individual Assignment | Group Assignment |
|---|---|
| Must update every time someone joins | Add to group = instant access |
| Must remove manually when someone leaves | Remove from group = instant revocation |
| Hard to audit — scattered across resources | Easy to audit — all in one group |
| Risk of forgotten assignments | Clean and consistent |
| Does not scale for large organizations | Scales perfectly |

### Key Rule
> Create user → Add to group → Group has role. Never skip the group step.

### Exam Question
**Q: A new employee needs access to 3 resource groups immediately. What is the correct process?**
A: Create their user account in Entra ID. Add them to the appropriate security group that already has role assignments on those resource groups. They automatically inherit all permissions. Never assign roles directly to the individual user because it does not scale and is hard to manage when they leave.

---

## Summary Table — 5 Scenarios at a Glance

| Scenario | Problem | Key Tool | Solution |
|---|---|---|---|
| 1 | Access Denied | Access Control (IAM) | Check role scope + Deny assignments |
| 2 | MFA Lockout | Authentication Methods | Issue Temporary Access Pass |
| 3 | Wrong Permissions | Access Control (IAM) | Change Contributor to Reader + Resource Lock |
| 4 | Guest No Access | External Identities | Verify invitation accepted + assign Reader role |
| 5 | New Employee | Entra ID Groups | Create user → Add to group → inherit permissions |

## Wednesday Score: 4/5 — 80% ✅

### What I got right
- Temporary Access Pass for MFA lockout ✅
- Contributor → Reader for wrong permissions ✅
- Resource Lock as extra protection ✅
- Guest user = external organization user ✅
- Groups over individual assignments ✅

### What to remember
- Access Denied = always check scope AND Deny assignments — not just role existence
- Guest user must accept invitation first before any access works
- Always check the invitation status (Accepted vs Pending) before assigning roles
