# Troubleshooting Scenarios

## Problem 1: "Wi-Fi says connected but I can't access the internet"
First, check your IP address using ipconfig. If the IP starts with 169.254, that means DHCP failed and your device didn't get a proper IP. Try releasing and renewing with ipconfig /release then ipconfig /renew. If you have a normal IP, try pinging your gateway (the address shown in ipconfig as Default Gateway). If the gateway doesn't respond, the problem is between you and your router. If the gateway responds, try pinging 8.8.8.8. If that works, try pinging google.com. If 8.8.8.8 works but google.com fails, your DNS is broken. Try changing your DNS to 8.8.8.8 in your network settings.
Copy and paste the following into your troubleshooting scenario file (e.g., `01-networking/troubleshooting-scenario.md`). 



**Problem 1**:


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

### Summary of Commands Used
| Command | Purpose |
|---------|---------|
| `ipconfig /all` | Shows IP configuration, gateway, DNS |
| `ipconfig /release` | Releases current IP (DHCP) |
| `ipconfig /renew` | Requests a new IP from DHCP |
| `ping <gateway>` | Tests connection to local router |
| `ping 8.8.8.8` | Tests internet connectivity (by IP) |
| `ping google.com` | Tests DNS + internet connectivity |



## Problem 2: "My IP address starts with 169.254"
This is APIPA. It means your computer tried to get an IP from a DHCP server but couldn't reach one. Check if your network cable is plugged in properly. Check if the DHCP server (usually your router) is running. Try restarting your router. If on Wi-Fi, try forgetting the network and reconnecting.

## Problem 3: "Website opens when I type the IP address but not when I type the domain name"
This is a DNS problem. The DNS server is either unreachable or returning wrong results. Try nslookup for that domain. Try using a different DNS server (8.8.8.8 or 1.1.1.1). On Windows, try flushing DNS cache with ipconfig /flushdns.

## Problem 4: "I can ping 8.8.8.8 but I can't open any website"
Internet works but DNS doesn't. Or ports 80/443 are being blocked by a firewall or proxy. Check DNS with nslookup. Check if a proxy is configured in browser settings. Check Windows Firewall rules.

## Problem 5: "Only one specific website is not opening, everything else works"
The website might be down (check from another device or use https://downdetector.com). Or the DNS record for that specific domain is wrong or cached wrong. Try flushing DNS. Try a different DNS server. Your ISP might be blocking it (common in Pakistan) — try using a VPN or different DNS.

## Problem 6: "VPN is connected but I can't access internal resources"
Check if VPN routes are configured properly. Is it a split tunnel VPN (only some traffic goes through VPN) or full tunnel (all traffic)? Check if DNS is pointing to the internal DNS server. Sometimes VPN connects but doesn't push the right routes.

## Problem 7: "RDP is not connecting to a remote server"
Check if port 3389 is open on the server. Check if the server's firewall allows RDP. Check if the server is running and reachable (ping it first). Check if Remote Desktop is enabled on the server in settings.

## Problem 8: "All users on the network are experiencing slow speeds"
Check bandwidth utilization. Run a speed test. Check if one device or user is consuming too much bandwidth. Check packet loss with ping -n 100 8.8.8.8 and see how many packets are lost. Check for network congestion during peak hours.
