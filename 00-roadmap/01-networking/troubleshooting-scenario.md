# Troubleshooting Scenarios

## Problem 1: "Wi-Fi says connected but I can't access the internet"
First, check your IP address using ipconfig. If the IP starts with 169.254, that means DHCP failed and your device didn't get a proper IP. Try releasing and renewing with ipconfig /release then ipconfig /renew. If you have a normal IP, try pinging your gateway (the address shown in ipconfig as Default Gateway). If the gateway doesn't respond, the problem is between you and your router. If the gateway responds, try pinging 8.8.8.8. If that works, try pinging google.com. If 8.8.8.8 works but google.com fails, your DNS is broken. Try changing your DNS to 8.8.8.8 in your network settings.
Copy and paste the following into your troubleshooting scenario file (e.g., `01-networking/troubleshooting-scenario.md`). 



## Problem 1: "Wi‑Fi says connected but I can't access the internet"

### Step‑by‑Step Diagnosis (Example Outputs)

1. **Check your IP configuration**  
   Run `ipconfig` in Command Prompt:


```markdown
C:\Windows\system32>ipconfig

Windows IP Configuration

Ethernet adapter Ethernet:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :

Wireless LAN adapter Local Area Connection* 11:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :

Wireless LAN adapter Local Area Connection* 12:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :

Ethernet adapter VMware Network Adapter VMnet1:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::2426:44dd:8c1a:9cd2%10
   IPv4 Address. . . . . . . . . . . : 192.168.184.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

Ethernet adapter VMware Network Adapter VMnet8:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::34ee:4999:2fe8:92b4%9
   IPv4 Address. . . . . . . . . . . : 192.168.118.1
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . :

Wireless LAN adapter Wi-Fi:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::97d7:5fe9:78a2:e582%21
   IPv4 Address. . . . . . . . . . . : 192.168.0.104
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.0.1

Ethernet adapter Bluetooth Network Connection:
   Media State . . . . . . . . . . . : Media disconnected
   Connection-specific DNS Suffix  . :
```

2. **Ping the default gateway**  
   `ping 192.168.0.1`

```
C:\Windows\system32>ping 192.168.0.1

Pinging 192.168.0.1 with 32 bytes of data:
Reply from 192.168.0.1: bytes=32 time=1ms TTL=64
Reply from 192.168.0.1: bytes=32 time=1ms TTL=64
Reply from 192.168.0.1: bytes=32 time=1ms TTL=64
Reply from 192.168.0.1: bytes=32 time=12ms TTL=64

Ping statistics for 192.168.0.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 12ms, Average = 3ms
```

3. **Ping an external IP (Google DNS)**  
   Use the correct Windows option `-n` for packet count.

```
C:\Windows\system32>ping -n 2 8.8.8.8

Pinging 8.8.8.8 with 32 bytes of data:
Reply from 8.8.8.8: bytes=32 time=55ms TTL=115
Reply from 8.8.8.8: bytes=32 time=117ms TTL=115

Ping statistics for 8.8.8.8:
    Packets: Sent = 2, Received = 2, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 55ms, Maximum = 117ms, Average = 86ms
```

4. **Ping a domain name (test DNS)**  
   `ping -n 2 google.com`

```
C:\Windows\system32>ping -n 2 google.com

Pinging google.com [142.250.202.238] with 32 bytes of data:
Reply from 142.250.202.238: bytes=32 time=36ms TTL=115
Reply from 142.250.202.238: bytes=32 time=35ms TTL=115

Ping statistics for 142.250.202.238:
    Packets: Sent = 2, Received = 2, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 35ms, Maximum = 36ms, Average = 35ms
```

**Interpretation:**  
- The Wi‑Fi adapter has a valid IP (`192.168.0.104`) and gateway (`192.168.0.1`).  
- The gateway responds to ping, so the local network is fine.  
- External IP (`8.8.8.8`) responds, so internet connectivity exists.  
- Domain name (`google.com`) resolves and responds, so DNS is working.  

In this example, there is **no actual connectivity problem** – the commands confirm that the internet is reachable. If you were experiencing “no internet,” the symptoms would differ (e.g., gateway unreachable, failed ping to 8.8.8.8, or DNS failure).



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
