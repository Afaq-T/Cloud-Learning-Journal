
# Troubleshooting Scenarios – Solutions

---

## Problem 1: "Wi‑Fi says connected but I can't access the internet"

### Troubleshooting Steps

1. **Check your IP address**  
   Open Command Prompt and run:
   ```
   ipconfig /all
   ```
   - Look at the **IPv4 Address** of your Wi‑Fi adapter.
   - **If it starts with 169.254.x.x** → This is an APIPA address. It means your device failed to get a valid IP from the DHCP server (usually your router).  
     **Fix:** Release and renew the IP:
     ```
     ipconfig /release
     ipconfig /renew
     ```
   - **If you have a normal IP** (like 192.168.x.x or 10.x.x.x) → Move to the next step.

2. **Test connectivity to your router (default gateway)**  
   In the same `ipconfig` output, find the **Default Gateway** address (e.g., 192.168.1.1). Then ping it:
   ```
   ping <gateway-address>
   ```
   - **If the gateway does NOT respond** → The problem is between your device and the router. Check your Wi‑Fi signal, restart the router, or check cables.
   - **If the gateway responds** → Your local network is working. Move to step 3.

3. **Test internet connectivity by pinging an external IP**  
   Ping Google’s public DNS server:
   ```
   ping 8.8.8.8
   ```
   - **If this fails** → Your internet connection is down. This could be an ISP outage, modem issue, or problem with your router’s internet link. Restart your modem and router.
   - **If this works** → Your internet is up, but there might be a DNS problem. Move to step 4.

4. **Test DNS resolution**  
   Ping a domain name, e.g.:
   ```
   ping google.com
   ```
   - **If this fails** (but step 3 worked) → Your DNS is broken.  
     **Fix:** Change your DNS server to a public one like Google’s (8.8.8.8) in your network adapter settings.
   - **If this works** → Congratulations, your internet is fully functional! If you still can't browse, check browser settings, proxy, or firewall.

---

## Problem 2: "My IP address starts with 169.254"

### Troubleshooting Steps

1. **Understand what 169.254 means**  
   This is an **APIPA** (Automatic Private IP Addressing) address. Your computer tried to get an IP from a DHCP server but couldn’t reach one.

2. **Check physical connection**  
   - If using Ethernet, ensure the cable is plugged in securely.
   - If using Wi‑Fi, check that you are connected to the correct network and have a strong signal.

3. **Restart your router**  
   - Unplug the router’s power, wait 30 seconds, and plug it back in. Wait a few minutes for it to fully restart.

4. **Renew your IP address**  
   Open Command Prompt as administrator and run:
   ```
   ipconfig /release
   ipconfig /renew
   ```
   - If this succeeds, you’ll get a normal IP (e.g., 192.168.x.x).

5. **Check if the DHCP server is running**  
   - Log into your router’s admin page (usually 192.168.1.1 or 192.168.0.1) and verify that DHCP is enabled.

6. **If on Wi‑Fi, forget and reconnect**  
   - Go to Wi‑Fi settings, forget the network, and reconnect by entering the password again.

7. **Still stuck?**  
   - Try connecting another device (phone, laptop) to the same network. If that device also gets a 169.254 address, the problem is likely the router. If only your computer has the issue, there may be a problem with your network adapter driver.

---

## Problem 3: "Website opens when I type the IP address but not when I type the domain name"

### Troubleshooting Steps

1. **Identify the problem**  
   This is a classic **DNS failure**. Your computer can reach the internet (since it loads the site by IP) but cannot resolve domain names to IP addresses.

2. **Test with nslookup**  
   Open Command Prompt and run:
   ```
   nslookup google.com
   ```
   - If it returns an IP address, DNS is working for that domain.
   - If it times out or returns an error, your DNS server is unreachable or misconfigured.

3. **Try a different DNS server**  
   - Temporarily change your DNS to a public server like Google’s (8.8.8.8) or Cloudflare’s (1.1.1.1).
   - In Windows: Go to Network Settings → Change adapter options → Right‑click your connection → Properties → Internet Protocol Version 4 (TCP/IPv4) → Use the following DNS server addresses → enter 8.8.8.8 and 8.8.4.4.

4. **Flush the DNS cache**  
   ```
   ipconfig /flushdns
   ```
   This clears any corrupted or outdated DNS records stored locally.

5. **Check the hosts file**  
   - Open `C:\Windows\System32\drivers\etc\hosts` in Notepad (as administrator).  
   - Ensure there are no unusual entries for the domain you’re trying to reach (e.g., `127.0.0.1 google.com` would block it).

6. **Restart the DNS Client service**  
   ```
   net stop dnscache
   net start dnscache
   ```

7. **If the problem persists**  
   - Check if your router is using a custom DNS that might be failing. Log into the router and change its DNS settings to 8.8.8.8 as well.

---

## Problem 4: "I can ping 8.8.8.8 but I can't open any website"

### Troubleshooting Steps

1. **Confirm the symptom**  
   - `ping 8.8.8.8` works → Internet connectivity is fine.
   - But browsers show “no internet” or can’t load any website.

2. **Check DNS**  
   Run:
   ```
   nslookup google.com
   ```
   - If this fails, DNS is the problem (see Problem 3 solutions).
   - If it resolves, DNS is working; move to the next step.

3. **Check if ports 80/443 are blocked**  
   - Try accessing a site by IP and port, e.g., `http://142.250.185.46` (Google’s IP). If that loads, DNS is fine but maybe your browser is using a proxy.
   - Use `telnet` to test port 80:
     ```
     telnet google.com 80
     ```
     If it connects (blank screen), the port is open. If it fails, the port is blocked.

4. **Check browser proxy settings**  
   - In Windows, go to Settings → Network & Internet → Proxy. Ensure “Use a proxy server” is off unless you actually use one.

5. **Check Windows Firewall**  
   - Open Windows Defender Firewall → Advanced settings → Outbound Rules. Look for rules blocking HTTP (port 80) or HTTPS (port 443). Temporarily disable the firewall to test, but re‑enable it afterward.

6. **Check for malware**  
   - Some malware modifies browser settings or host files. Run a quick scan with Windows Defender or Malwarebytes.

7. **Reset network stack**  
   Open Command Prompt as administrator and run:
   ```
   netsh int ip reset
   netsh winsock reset
   ```
   Then restart your computer.

---

## Problem 5: "Only one specific website is not opening, everything else works"

### Troubleshooting Steps

1. **Check if the website is down for everyone**  
   - Use a service like https://downforeveryoneorjustme.com or https://downdetector.com. Enter the URL to see if it’s a global outage.

2. **Flush DNS cache**  
   ```
   ipconfig /flushdns
   ```
   This removes any outdated DNS record for that specific domain.

3. **Try a different DNS server**  
   - Switch to 8.8.8.8 (Google) or 1.1.1.1 (Cloudflare) as described in Problem 3.

4. **Check the hosts file**  
   - Open `C:\Windows\System32\drivers\etc\hosts` and ensure there’s no entry blocking that domain (e.g., `127.0.0.1 example.com`). If found, delete or comment it out (add `#` at the beginning).

5. **Clear browser cache and cookies**  
   - In your browser, clear browsing data for that site. Sometimes cached redirects or corrupted cookies cause issues.

6. **Try accessing via a different browser or device**  
   - If the site opens on another device, the problem is local to your computer.
   - If it doesn’t open on any device, the issue is likely with the website or your ISP.

7. **Check if your ISP is blocking the site**  
   - This is common in some regions. Try using a VPN or changing your DNS to a public one (which might bypass the block).
   - If a VPN works, your ISP is likely blocking the site.

8. **Check for browser extensions**  
   - Disable all extensions and try again. Some ad‑blockers or privacy extensions may block certain sites.

---

## Problem 6: "VPN is connected but I can't access internal resources"

### Troubleshooting Steps

1. **Verify VPN connection status**  
   - Check that the VPN client shows “Connected” and has an assigned IP address (usually a private IP like 10.x.x.x or 172.16.x.x).

2. **Check routes**  
   - Open Command Prompt and run:
     ```
     route print
     ```
   - Look for routes pointing to the internal network (e.g., 10.10.10.0/24). If missing, the VPN isn’t pushing the correct routes.

3. **Determine tunnel type**  
   - **Split tunnel**: Only traffic destined for the internal network goes through the VPN; internet traffic goes directly.
   - **Full tunnel**: All traffic goes through the VPN.  
   - Check with your VPN administrator if you’re unsure which type you have.

4. **Test connectivity to internal resources by IP**  
   - Ping the internal server by IP (e.g., `ping 10.10.10.5`).  
   - If IP works but hostname doesn’t, it’s a DNS issue (next step).

5. **Check DNS for internal resources**  
   - After connecting, run:
     ```
     nslookup internal-server-name
     ```
   - If it fails, the VPN may not be pushing the internal DNS server. You may need to manually add the DNS server in your adapter settings.

6. **Check firewall rules**  
   - On the internal server, ensure the firewall allows traffic from the VPN subnet.  
   - On your local machine, check Windows Firewall to ensure it’s not blocking outbound traffic to the internal network.

7. **Reinstall or update VPN client**  
   - Sometimes outdated clients cause routing or DNS issues. Check with your IT department for the correct version.

8. **Check VPN logs**  
   - Look at the VPN client logs for errors. Common errors include “No routes received” or “DNS configuration failed.”

---

## Problem 7: "RDP is not connecting to a remote server"

### Troubleshooting Steps

1. **Verify the server is reachable**  
   - Ping the server by IP:
     ```
     ping <server-ip>
     ```
   - If ping fails, the server may be offline or network connectivity is broken.

2. **Check if the server is running**  
   - If you have access to the server console (physically or via a management portal like Azure/Hyper‑V), ensure the VM or physical server is powered on.

3. **Check if RDP is enabled on the server**  
   - On the server, go to **System Properties** → **Remote** tab → Ensure **“Allow remote connections to this computer”** is selected.
   - If you’re using a non‑standard port, note the port number.

4. **Check firewall rules on the server**  
   - Ensure Windows Firewall (or any third‑party firewall) allows inbound connections on **port 3389** (or the custom RDP port).
   - On the server, run:
     ```
     netsh advfirewall firewall show rule name="Remote Desktop"
     ```
   - If the rule is missing, create it:
     ```
     netsh advfirewall firewall add rule name="RDP" dir=in action=allow protocol=TCP localport=3389
     ```

5. **Check network security groups (if in Azure)**  
   - If the server is in Azure, check the **NSG** rules attached to the VM’s subnet or network interface. Ensure an inbound rule allows TCP port 3389 from your IP (or from the internet if you’re connecting directly).

6. **Check the local client firewall**  
   - Temporarily disable Windows Firewall on your client machine to see if it’s blocking outbound RDP.

7. **Try connecting by IP instead of hostname**  
   - If hostname fails but IP works, it’s a DNS issue. Use the IP address or update your hosts file.

8. **Check for Network Level Authentication (NLA)**  
   - If the server requires NLA and your client doesn’t support it, you may get an error. You can disable NLA on the server (but this reduces security) or update your client.

9. **Look at Event Viewer on the server**  
   - On the server, open Event Viewer → Windows Logs → System. Look for errors related to Remote Desktop Services (event ID 1024, 1025, etc.).

10. **Restart the Remote Desktop Services**  
    On the server, run as administrator:
    ```
    net stop termservice
    net start termservice
    ```

---

## Problem 8: "All users on the network are experiencing slow speeds"

### Troubleshooting Steps

1. **Run a speed test**  
   - From a wired client (if possible), go to https://speedtest.net and check download/upload speeds and ping. Compare with your expected speeds from your ISP.

2. **Check bandwidth utilization**  
   - If you have access to the router, log in and look at the **traffic statistics** or **bandwidth monitoring** page. Identify which devices are using the most bandwidth.
   - On a Windows PC, you can use **Resource Monitor** (resmon.exe) → Network tab to see which processes are using the network.

3. **Check for packet loss**  
   - Open Command Prompt and run:
     ```
     ping -n 100 8.8.8.8
     ```
   - After it completes, look at the percentage of lost packets. Even 1–2% loss can cause noticeable slowness.

4. **Check for network congestion**  
   - If slowness happens only during peak hours (evenings), it may be ISP congestion. Test at different times of day to confirm.

5. **Check for a single device hogging bandwidth**  
   - Look for devices doing large downloads, streaming 4K video, or running backups. Pause those activities temporarily to see if speed improves.

6. **Restart the router and modem**  
   - Unplug both, wait 30 seconds, plug the modem back in first, wait for it to fully boot, then plug the router back in. This clears temporary issues.

7. **Check for interference (Wi‑Fi)**  
   - If users are on Wi‑Fi, check the Wi‑Fi channel. Use a Wi‑Fi analyzer app to see if neighboring networks are causing interference. Change the channel on your router.

8. **Check for outdated firmware**  
   - Log into the router and check for firmware updates. An update can fix performance bugs.

9. **Check for malware on a user’s PC**  
   - A single infected PC can generate massive background traffic. Run a malware scan on suspicious devices.

10. **Contact your ISP**  
    - If all else fails and you’ve ruled out internal issues, contact your ISP. They can check for line problems, outages, or signal issues.

---

