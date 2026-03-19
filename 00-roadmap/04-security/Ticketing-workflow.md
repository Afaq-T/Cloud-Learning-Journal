# Ticketing Workflow

## Full Ticket Lifecycle

```
New → Assigned → In Progress → Waiting → Resolved → Closed
```

### Stage 1 — New
Ticket created by user or monitoring system. Nobody has acted on it yet. SLA clock starts immediately.

### Stage 2 — Assigned
Ticket picked up and assigned to a specific engineer. Engineer has reviewed and understood the issue.

### Stage 3 — In Progress
Engineer is actively working. Updates should be added every 30-60 minutes for critical issues. All actions must be documented in ticket notes.

### Stage 4 — Waiting
Engineer is blocked — waiting on customer information, another team, vendor support, or a change window. SLA clock may pause depending on company policy.

### Stage 5 — Resolved
Fix applied. Customer notified and asked to confirm. Ticket stays Resolved until customer confirms — not Closed yet.

### Stage 6 — Closed
Customer confirmed the fix works. Or auto-closed after set number of days with no response. All resolution notes documented. Final stage.

---

## 4 Priority Levels with SLA Time Targets

### P1 — Critical (Urgent)
**Definition:** Entire service or system completely down for all users. No workaround available.

**Examples:**
- Production server down — 100+ users cannot work
- Company email completely offline
- VPN down for entire remote workforce

**Response time:** Immediate — within 15 minutes
**Resolution target:** Within 4 hours
**Communication:** Update ticket every 30 minutes. Notify management immediately.

---

### P2 — High
**Definition:** Major feature broken for many users. Significant business impact. Workaround may exist but is not ideal.

**Examples:**
- VPN not connecting for remote team of 20 people
- SharePoint down for one department
- MFA broken for a group of users

**Response time:** Within 1 hour
**Resolution target:** Within 4 hours
**Communication:** Update ticket every hour. Notify team lead.

---

### P3 — Medium
**Definition:** Single user or small group affected. Partial impact. Workaround exists, business can continue.

**Examples:**
- Single user cannot access SharePoint
- One person's email not syncing
- Software installation request

**Response time:** Within 4 hours
**Resolution target:** Within 1 business day
**Communication:** Update when status changes. Daily update if unresolved.

---

### P4 — Low
**Definition:** Minor issue with no business impact. Cosmetic issues, requests, or questions.

**Examples:**
- New employee account setup (planned in advance)
- Password reset request (user can still work)
- Training request

**Response time:** Within 8 hours
**Resolution target:** Within 1 week
**Communication:** Update when work begins and when resolved.

---

## Priority Summary Table

| Priority | Name | Who is affected | Response Time | Resolution Target |
|---|---|---|---|---|
| **P1** | Critical | All users — complete outage | 15 minutes | 4 hours |
| **P2** | High | Many users — major feature down | 1 hour | 4 hours |
| **P3** | Medium | Single user — workaround exists | 4 hours | 1 business day |
| **P4** | Low | No business impact — request | 8 hours | 1 week |

---

## Escalation Criteria — When to Escalate

Escalate to team lead or senior engineer when ANY of these are true:

**1 — SLA breach approaching**
Cannot resolve within the target time. Escalate before the SLA is breached, not after.

**2 — Beyond your skill level**
Issue requires knowledge, tools, or access you do not have. Never guess on production systems.

**3 — Customer requests escalation**
Respect the request immediately. Document it in the ticket.

**4 — Issue is growing**
What started as one user is now affecting more. Reclassify to higher priority if needed.

**5 — Security incident suspected**
Any suspected breach, unauthorized access, or data leak becomes P1 immediately — escalate regardless of original priority.

**6 — Production change required**
Any change to production systems during business hours requires team lead or change management approval.

---

## Escalation Process

1. Add note to ticket explaining why you are escalating and what you have already tried
2. Change ticket assignee to the escalation contact
3. Notify them directly — do not rely on ticket notification alone. Call or message them
4. Brief them: what is the issue, who is affected, what you tried, what you need
5. Stay available to assist — do not abandon the ticket

---

## Good Ticket Documentation

Every note should answer:
- **What did you do?** (exact steps taken)
- **What was the result?** (what happened after)
- **What is the next step?** (what you plan to do next)

### Bad note
> "Checked the user's account. Still not working."

### Good note
> "Checked user's RBAC role assignments in Access Control (IAM) on Resource Group rg-prod. User has Reader role at subscription level but there is a Deny assignment on the storage account created by policy on 2026-03-10. Contacted the policy owner team to request an exception. Waiting for their response — estimated 2 hours."

---

## Freshdesk Quick Actions

| Action | How |
|---|---|
| Create ticket | New Ticket → fill subject, description, priority |
| Assign ticket | Click Agent field → select engineer |
| Update status | Click Status dropdown → select new status |
| Add internal note | Click Reply → type update → Add Note |
| Change priority | Click Priority dropdown |
| Escalate | Change assignee + notify new assignee directly |
| Resolve | Change status to Resolved + notify customer |
| Close | Change status to Closed after customer confirms |
