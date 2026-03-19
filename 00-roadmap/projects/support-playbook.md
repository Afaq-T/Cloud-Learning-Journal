# IT Support Playbook


## FORMAT:

**Issue:** [Short descriptive name]

**Symptoms:** [What the user experiences]

**Steps to Troubleshoot:**
1. [Command or action]
2. [Next step based on result]
3. [Continue until root cause found]
**Resolution:** [What fixes the issue]

**When to Escalate:** [When to pass to higher‑level support]



## Issue: Wi-Fi Connected But No Internet
**Symptoms:** User reports Wi-Fi icon shows connected, but browsers show "No Internet"
**Steps to Troubleshoot:**
1. Open CMD → type `ipconfig /all`
2. Check IP address — if `169.254.x.x` → DHCP problem
3. If normal IP → ping default gateway
4. If gateway responds → ping `8.8.8.8`
5. If `8.8.8.8` responds → ping `google.com`
6. If `google.com` fails → DNS issue → change DNS to `8.8.8.8`
**Resolution:** Depends on which step fails
**When to Escalate:** If gateway is unreachable and reboot doesn't fix it, escalate to network team

---

## Issue: DHCP Failure (169.254.x.x IP)
**Symptoms:** User has no internet; `ipconfig` shows IP starting with 169.254.x.x
**Steps to Troubleshoot:**
1. Run `ipconfig /release` then `ipconfig /renew`
2. If still 169.254 → restart router
3. Check physical connections (cable/Wi‑Fi)
4. If on Wi‑Fi, forget network and reconnect
**Resolution:** Successful DHCP lease
**When to Escalate:** If router restart fails, check if DHCP server is running on router; escalate if router configuration needed

---

## Issue: DNS Failure (Can't Resolve Names)
**Symptoms:** Can ping `8.8.8.8` but cannot browse by domain name
**Steps to Troubleshoot:**
1. Run `nslookup google.com` – if fails, DNS is down
2. Flush DNS cache: `ipconfig /flushdns`
3. Change DNS server to `8.8.8.8` in network settings
4. If still fails, check router's DNS settings
**Resolution:** Correct DNS configuration
**When to Escalate:** If multiple devices affected, router may need replacement or ISP contact

---

## Issue: Slow Network / High Latency
**Symptoms:** Web pages load slowly, videos buffer
**Steps to Troubleshoot:**
1. Run speed test (fast.com or speedtest.net)
2. Check for packet loss: `ping -n 50 8.8.8.8`
3. Identify bandwidth hogs (Windows Resource Monitor)
4. Restart modem/router
5. Check Wi‑Fi interference (change channel if possible)
**Resolution:** Optimize network usage or upgrade plan
**When to Escalate:** If all devices slow and reboot doesn't help, ISP issue

---

## Issue: Port Blocked (e.g., Can't Access Specific Service)
**Symptoms:** Application can't connect, but internet works
**Steps to Troubleshoot:**
1. Verify which port is required (e.g., 3389 for RDP)
2. Test port with `telnet <server> <port>` or online port checker
3. Check Windows Firewall → Advanced Settings → Inbound Rules
4. If on corporate network, check with network team
**Resolution:** Open the port in firewall or adjust application
**When to Escalate:** If firewall rule exists but still blocked, deeper network policy may be involved

---

## Issue: Can't RDP to Remote Server
**Symptoms:** Remote Desktop connection fails or times out
**Steps to Troubleshoot:**
1. Ping server by IP – if unreachable, network issue
2. If ping works, check if RDP port (3389) is open: `telnet <server> 3389`
3. Verify Remote Desktop is enabled on the server
4. Check Windows Firewall on server allows RDP
5. If in Azure, check NSG rules for port 3389
**Resolution:** Enable RDP or open firewall port
**When to Escalate:** If server is in cloud/DC, may need admin access

---

## Issue: VPN Connected But Can't Access Internal Resources
**Symptoms:** VPN shows connected, but can't ping internal servers or access intranet
**Steps to Troubleshoot:**
1. Check VPN-assigned IP (usually a private IP)
2. Run `route print` to see if routes to internal networks exist
3. Ping internal server by IP – if works, DNS issue
4. If IP fails, check if split tunnel vs full tunnel
5. Verify internal DNS is pushed by VPN
**Resolution:** Correct routing or DNS settings
**When to Escalate:** If routes are missing, VPN configuration may need update

---

## Issue: Printer Not Reachable on Network
**Symptoms:** Users can't print, printer is offline
**Steps to Troubleshoot:**
1. Check printer's network connection (cable or Wi‑Fi)
2. Ping printer's IP address from a PC
3. If ping fails, restart printer
4. Check if printer is on same subnet as PCs
5. Verify printer is not in power save mode
**Resolution:** Printer back online
**When to Escalate:** If printer is on but unreachable, may need network team to check switch port/VLAN

---

## Issue: No Ethernet Connection (Cable Unplugged or Faulty)
**Symptoms:** User reports no network access; Ethernet icon shows a red "X" or "Unplugged"; link lights on the network card or switch port are off.
**Steps to Troubleshoot:**
1. Check physical connection – ensure the Ethernet cable is securely plugged into both the computer and the wall jack/switch.
2. Try a different cable – if available, swap with a known‑good cable.
3. Check link lights – on the computer’s Ethernet port and on the switch port (if accessible). No light indicates a physical layer issue.
4. On Windows, run `ipconfig /all` – if the adapter shows "Media disconnected", the problem is physical.
5. If using a docking station or USB adapter, try re‑seating it or connecting directly to the laptop’s built‑in port.
6. Restart the computer – sometimes the network adapter driver gets stuck.
7. If the issue persists on multiple cables and ports, the network adapter may be faulty. Try updating the driver or using a different device to test the wall jack.
**Resolution:** Re‑establish physical connectivity – either by fixing the cable, re‑seating connections, or replacing faulty hardware.
**When to Escalate:** If the wall jack itself is dead (tested with another device) or if the network adapter is confirmed faulty (requires hardware replacement), escalate to facilities or IT hardware team.

---

## Issue: Wi‑Fi Network Not Visible in List
**Symptoms:** User cannot see their home or office Wi‑Fi network in the list of available networks, even though other networks appear.
**Steps to Troubleshoot:**
1. Verify Wi‑Fi is turned on – check the physical switch (on laptops) or the software toggle in Windows (Action Center > Wi‑Fi).
2. Run the networking troubleshooter: right‑click the network icon → Troubleshoot problems.
3. Check if the hidden network is set to not broadcast its SSID. If you know the SSID, manually add the network:  
   *Settings → Network & Internet → Wi‑Fi → Manage known networks → Add a new network* – enter the exact SSID and security type.
4. Restart the Wi‑Fi adapter:  
   `netsh interface set interface name="Wi‑Fi" admin=disable`  
   `netsh interface set interface name="Wi‑Fi" admin=enable`
5. Check for interference – if the network is on a 5 GHz band and the client is far from the router, try moving closer.
6. Update the Wi‑Fi driver – Device Manager → Network adapters → right‑click Wi‑Fi adapter → Update driver.
7. Check if the router is broadcasting the SSID – log into the router and ensure "SSID Broadcast" is enabled.
**Resolution:** Wi‑Fi network becomes visible again.
**When to Escalate:** If the router settings are correct but the network still doesn't appear, the router may need replacement; involve the network team.

---

## Issue: IP Address Conflict
**Symptoms:** User gets a pop‑up "Windows has detected an IP address conflict"; they have no network access or intermittent connectivity.
**Steps to Troubleshoot:**
1. Open Command Prompt as administrator and run `ipconfig /release` then `ipconfig /renew`.
2. If the conflict persists, run `ipconfig /all` and note the IP address that is conflicting.
3. On the network, find the device that is using that same IP. You can use `arp -a` to see recent MAC‑to‑IP mappings.
4. Check the DHCP server (usually the router) to see if there is a static reservation that conflicts with the dynamic pool.
5. If the user has a static IP assigned, change it to a different unused IP or switch to DHCP.
6. Clear the ARP cache on the local machine: `arp -d *` (admin prompt).
7. Restart both the computer and the router to clear any stuck leases.
**Resolution:** Each device gets a unique IP address.
**When to Escalate:** If the conflict is caused by misconfigured network infrastructure (e.g., rogue DHCP server), escalate to the network team.

---

## Issue: Network Drive Mapping Fails
**Symptoms:** User tries to map a network drive (e.g., `\\server\share`) but gets an error like "Network path not found" or "Access denied".
**Steps to Troubleshoot:**
1. Verify the user can reach the server by IP: `ping <server‑IP>`. If ping fails, the server may be down or unreachable.
2. If ping works, try accessing the share by IP instead of name: `\\<server‑IP>\share`. If that works, it’s a DNS or name resolution issue.
3. Check if the user has permissions to the share – verify with the server administrator or check share/NTFS permissions.
4. On the client, ensure the Workstation service is running:  
   `net start workstation`
5. Check if the required ports are open (SMB uses 445). Test with:  
   `Test-NetConnection <server> -Port 445` (PowerShell).
6. If the server is in a different domain or workgroup, ensure credentials are correct. Use `net use Z: \\server\share /user:DOMAIN\username *` to map with explicit credentials.
7. Check Windows Firewall on both client and server to ensure File and Printer Sharing is allowed.
8. Restart the "TCP/IP NetBIOS Helper" service if NetBIOS is required.
**Resolution:** User successfully maps the network drive.
**When to Escalate:** If the server itself is unreachable or permissions need to be changed by the server admin, escalate to the appropriate team.

---

## Section: Identity & Access Management (IAM)

---

## Issue: User Gets Access Denied on a Resource

**Symptoms:** User reports "Access Denied" or "You do not have permission" when opening an Azure resource. Manager confirms they should have access.

**Steps to Troubleshoot:**
1. Go to the resource in Azure portal → click **Access Control (IAM)** → **Role Assignments** tab
2. Look for the user directly — if not listed, check if they are in any groups that have role assignments
3. Check the **scope** of the role — a role assigned to Resource Group A does not apply to Resource Group B
4. Click **Deny assignments** tab — check if a Deny assignment exists on the resource
5. Confirm the user is signed in with the correct account (work vs personal Microsoft account)
6. Check if the user account is enabled in Entra ID → Users → check account status

**Resolution:** If role missing — assign appropriate role (Reader or Contributor) at the correct scope. If Deny assignment exists — contact policy owner for exception. If wrong account — guide user to sign in with work account.

**When to Escalate:** Escalate if Deny assignment needs removal (policy owner approval required). Escalate if issue affects many users — may be a policy change affecting everyone.

---

## Issue: MFA Lockout — User Cannot Sign In

**Symptoms:** User cannot sign in because MFA is required but their phone is lost, broken, or inaccessible.

**Steps to Troubleshoot:**
1. Verify the user's identity through secondary method (manager confirmation, HR records)
2. Go to **Entra ID** → **Users** → find the user → click **Authentication Methods**
3. Click **+ Add authentication method** → select **Temporary Access Pass**
4. Set duration (recommend 1 hour) → click Add
5. Give the TAP code to the user through a secure channel (phone call — not email)
6. User signs in with TAP → immediately goes to aka.ms/mysecurityinfo → registers new MFA device
7. TAP expires automatically after the set time

**Resolution:** Temporary Access Pass restores immediate access without compromising security. After new device is registered, user proceeds with normal MFA.

**When to Escalate:** Never issue a TAP without verifying identity first. Escalate if user says they never set up MFA but system requires it — may be a policy enforcement issue.

---

## Issue: User Has Wrong Permissions — Can Modify When Should Only View

**Symptoms:** A user is accidentally modifying or deleting resources. Investigation shows they should only be able to view, not change anything.

**Steps to Troubleshoot:**
1. Go to the resource group → **Access Control (IAM)** → **Role Assignments**
2. Find the user or their group — note the current role (likely Contributor)
3. Click three dots next to the assignment → **Remove** → confirm removal
4. Click **Add** → **Add role assignment** → select **Reader**
5. Assign Reader to the user's group (not directly to the individual user)
6. Verify in Role Assignments tab that Reader is assigned and Contributor is removed
7. Apply a **Delete Resource Lock** on any critical resources for extra protection

**Resolution:** Change Contributor to Reader. Add Delete Resource Lock on production resources so even Contributor cannot accidentally delete them.

**When to Escalate:** Escalate if resources were already deleted — may require backup restoration. Escalate to management if wrong permissions were assigned deliberately.

---

## Issue: Guest User Cannot Access Shared Resources

**Symptoms:** A partner company consultant accepted an invitation email but cannot see any Azure resources or shared content.

**Steps to Troubleshoot:**
1. Go to **Entra ID** → **External Identities** → find the guest user
2. Check their **Status** — must show **Accepted** not **Pending**
3. If Pending — resend the invitation. Guest must accept before any access works
4. Once Accepted — go to the specific resource → **Access Control (IAM)** → assign Reader role to the guest user
5. Check if any **Conditional Access policies** block external users (device compliance, location restrictions)
6. Guide guest to sign in at portal.azure.com using their own organization's credentials

**Resolution:** Resend invitation if Pending. Assign Reader role on specific resources needed. Create Conditional Access exception if policy is blocking them.

**When to Escalate:** Escalate if Conditional Access policy needs modification (security team approval). Escalate if guest needs access beyond Reader (management approval for external user privileges).

---

## Issue: New Employee Needs Access to Multiple Resources

**Symptoms:** New employee joins and needs immediate access to multiple resource groups and applications from day one.

**Steps to Troubleshoot:**
1. Confirm new employee details with HR — name, email, department, start date
2. Create **user account** in Entra ID → Users → New user → set temporary password
3. Find the appropriate **security group** for their department (e.g. grp-it-team)
4. Add new user to the group → Members → Add members → search and select
5. Verify the group already has correct role assignments on the needed resource groups
6. If group lacks access to a needed resource — add role assignment to the group (never to the individual)
7. Send temporary credentials through secure channel (through manager — not email)
8. Confirm user can sign in and access resources on their first day

**Resolution:** Group membership gives instant access to all resources the group has. No individual role assignments needed. When they leave — remove from group and disable account immediately.

**When to Escalate:** Escalate if new employee needs Owner or higher access (management approval required). Escalate if no appropriate group exists and one needs to be created (security team involvement).

---
