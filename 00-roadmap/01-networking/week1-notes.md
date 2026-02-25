# Network Types and Topologies – Simple Notes

## What is a network?
- A group of connected devices (computers, printers, servers, switches, etc.) that can talk to each other.

## Network Types (by size)

### PAN (Personal Area Network)
- Around one person – e.g., smartphone connected to smartwatch, laptop, tablet.
- Usually uses **Bluetooth** (short range, low power).

### LAN (Local Area Network)
- Covers a single location like an office, school, or home.
- Privately owned, needs permission to join.
- Most common type of network.
- Speeds: **10 Gbps or faster**.

### MAN (Metropolitan Area Network)
- Connects multiple locations in a city (like different offices of a company in the same city).
- Needs dedicated, secure connections between the LANs.

### WAN (Wide Area Network)
- Connects locations across cities, countries, or globally.
- Links many LANs together (e.g., head office + branch offices).
- Usually slower than LAN (less than 1 Gbps) and more congested.
- Often uses **VPN** (Virtual Private Network) for secure connections.

### Quick comparison: LAN vs WAN
| LAN                                | WAN                                   |
|------------------------------------|---------------------------------------|
| Private, usually one building      | Connects separate locations           |
| Very fast (10+ Gbps)               | Slower (under 1 Gbps)                 |
| Less traffic                       | More traffic                          |
| Managed in‑house                   | Often needs a third‑party provider    |
## Network Topologies (how devices are arranged)

### Bus Topology
- All devices connected to one main cable (the “bus”).
- **Simple** but **not reliable** – if the main cable breaks, the whole network fails.
- Only good for small, close‑together setups.

### Ring Topology
- Each device connects to its neighbour, forming a circle.
- More resilient than bus, but a break in the ring still causes problems.

### Mesh Topology
- **Full mesh**: every device connects directly to every other device (very reliable, but expensive and complex).
- **Partial mesh**: only some devices connect directly; others connect through one device.
- Most modern networks act like a **logical mesh** – any device can talk to any other, thanks to network protocols.

### Star Topology (most common)
- All devices connect to a central **hub or switch**.
- If one device fails, the rest still work.
- Easy to add new devices.
- Very robust and scalable – used in most homes and offices.

## Ethernet (the standard for wired networks)
- Defines how data is sent, errors are handled, and performance is measured.
- Works at the **physical** and **data link** layers of the OSI model.
- Based on the **IEEE 802.3** standard.

### Ethernet speeds
- **Fast Ethernet (802.3u)** – up to 100 Mbps (100BASE‑TX).
- **Gigabit Ethernet (802.3ab)** – up to 1000 Mbps (1 Gbps). Recommended for businesses.
- **10 Gigabit Ethernet (802.3ae)** – 10 Gbps, needs fibre optics.
- **Terabit Ethernet** – today up to 400 Gbps; future speeds of 800 Gbps and 1.6 Tbps are coming.

## Networks in Azure (cloud)
- **Azure Virtual Network** lets you build your own private network in the cloud, just like an on‑premises LAN.
- You can connect your on‑premises network to Azure using:
  - **VPN Gateway** – secure connection over the internet.
  - **ExpressRoute** – a private, dedicated, high‑speed connection (needs a partner provider).

These basics will help you understand how Azure networking works later!




# NEW TOPIC:
# Network Devices – Simple Notes

## Network Standards (The Rules)
- **Standards** make sure devices from different brands can work together.
- They are set by official bodies like **IEEE**, **ITU**, and **ANSI**.
- Without standards, your laptop might not connect to a random router.

### The 802 Family (Important IEEE Standards)
| Standard | Name | What it does |
|----------|------|--------------|
| 802.3 | Ethernet | Wired networking (copper or fiber cables) |
| 802.11 | Wi-Fi | Wireless networking |
| 802.11a/b/g/n/ac/ax | Wi-Fi versions | Faster speeds, better range over time |
| 802.15.1 | Bluetooth | Short-range device connection (phones, earbuds) |
| 802.15.4 | ZigBee | Smart home devices (low power, sensors) |
| 802.16 | WiMAX | Wireless MAN (like city-wide Wi-Fi) |

---

## MAC Address (Physical Address)
- Every network device has a **unique** MAC address (like a fingerprint).
- Format: `AA-6A-BA-2B-68-C1` (6 pairs of hex numbers)
- First 3 pairs = **Manufacturer** (e.g., AA-6A-BA = Cisco)
- Last 3 pairs = **Device ID** (unique to that device)
- You can see it in Windows by typing `ipconfig /all`

---

## Network Devices (The Hardware)

### 1. Repeater
- **Job:** Boosts the signal so it can travel longer distances.
- **How:** Regenerates the signal exactly as received (doesn't change or check it).
- **Use when:** Cables are too long and signal gets weak.

### 2. Hub
- **Job:** Connects multiple devices in a network.
- **How:** Sends incoming data to **all** connected devices (like shouting in a room).
- **Problem:** Wastes bandwidth, not secure, slow.
- **Types:**
  - **Fast Ethernet Hub:** For 100 Mbps networks.
  - **Dual-Speed Hub:** Can handle both 10 Mbps and 100 Mbps devices.
- **Status:** Rarely used now – replaced by switches.

### 3. Bridge
- **Job:** Divides a network into sections (segments).
- **How:** Uses MAC addresses to decide whether to forward data or not.
- **Benefit:** Reduces unnecessary traffic – keeps local traffic local.

### 4. Switch (Most Common Today)
- **Job:** Connects devices intelligently.
- **How:** Learns which device is on which port, sends data **only to the right device** (not everyone).
- **Benefit:** Fast, efficient, secure.
- **Full-Duplex:** Can send and receive at the same time.

#### Types of Switches
| Type | Description |
|------|-------------|
| **Unmanaged** | Plug and play – no setup. Good for home/small office. |
| **Managed** | Can configure VLANs, QoS, port mirroring, etc. Used in businesses. |
| **Smart** | Middle ground – web interface, some settings but not full control. |

#### Cool Switch Features
- **PoE (Power over Ethernet):** Powers devices like phones or cameras through the network cable.
- **VLAN:** Create separate virtual networks on the same physical switch.
- **QoS:** Give priority to important traffic (like video calls).
- **Port Mirroring:** Copy traffic to one port for monitoring/debugging.

### 5. Router
- **Job:** Connects **different networks** together (e.g., your home network to the internet).
- **How:** Uses **IP addresses** to forward data between networks.
- **Also called:** Gateway (default gateway is the router's IP).
- **Routing Table:** A list of paths to other networks.
- **Protocols:** Routers talk to each other using protocols like **BGP**.

#### Types of Routers
| Type | Where it's used |
|------|-----------------|
| **Access Router** | Home or small office (low cost, simple) |
| **Distribution Router** | Collects data from multiple routers, manages traffic |
| **Edge Router** | At the boundary between your network and the internet (has firewall, DHCP, DNS) |
| **Core Router** | In data centers, connects buildings, focuses on speed and reliability |

### 6. Wireless Router / Access Point
- **Wireless Router:** Normal router + Wi-Fi access point combined.
- **Access Point:** Just the Wi-Fi part (needs a router to work).
- **Wireless Modem:** The box your ISP gives you – converts ISP signal to Ethernet.
- Many home devices combine modem + router + switch + Wi-Fi in one box.

---

## Azure Networking Options

### Hub-Spoke Topology
- **Hub:** Central Azure VNet that connects to on-premises network.
- **Spokes:** Other VNets connected to the hub (like branches).
- Traffic between spokes goes through the hub (good for security and central management).

### Azure ExpressRoute
- **Private, dedicated connection** between your office and Azure.
- Faster and more reliable than a regular VPN.
- Uses a third-party provider to set up the circuit.




# NEW TOPIC:
# Network Protocols – Simple Notes

## What is a Network Protocol?
- A set of **rules** that devices follow to communicate with each other.
- Think of it like a language – if two devices don't speak the same protocol, they can't understand each other.
- Protocols handle: how to start communication, how to send data, how to handle errors.

## Key Terms to Know

### Network Address
- **MAC Address:** Hardware-level address (burned into the network card). Physical fingerprint.
- **IP Address:** Software-level address (like your device's mailing address on the internet).

### Data Packet
- A chunk of data sent over the network.
- Contains:
  - **Header:** Sender address, destination address, packet size, protocol, packet number.
  - **Data:** The actual content.
  - **Trailer:** Error checking info.
- Analogy: Mailing a book one page at a time – each envelope has enough info to reassemble later.

### Datagram
- Same as a packet, but usually refers to **unreliable** delivery (no guarantee it arrives).

### Routing
- The process of finding the best path for data to travel from sender to receiver across networks.

---

## Three Categories of Protocols

### 1. Communication Protocols (Sending/Receiving Data)

#### Foundational Protocols (The Basics)
| Protocol | Name | What it does |
|----------|------|--------------|
| **IP** | Internet Protocol | Handles **addressing** – adds sender/recipient IP addresses to packets. Doesn't guarantee delivery, just addresses. |
| **TCP** | Transmission Control Protocol | Makes sure data arrives **completely and in order**. Reliable but has overhead (slower). |
| **UDP** | User Datagram Protocol | Fast, **connectionless**, no guarantee of delivery. Used for streaming, gaming, VoIP where speed matters more than perfection. |

#### Application Protocols (What We Use Daily)
| Protocol | Name | What it does |
|----------|------|--------------|
| **HTTP** | Hypertext Transfer Protocol | Delivers web pages from server to browser. |
| **HTTPS** | HTTP Secure | Encrypted version of HTTP (uses SSL/TLS). |
| **FTP** | File Transfer Protocol | Upload/download files to/from a server. |
| **POP3** | Post Office Protocol | Receives emails (downloads to your device). |
| **SMTP** | Simple Mail Transfer Protocol | Sends emails. |
| **IMAP** | Internet Message Access Protocol | Manages emails on the server (keeps them synced across devices). |

---

### 2. Security Protocols (Keeping Data Safe)

| Protocol | What it does |
|----------|--------------|
| **SSL** | Secure Socket Layer – encrypts data between your computer and a server. |
| **TLS** | Transport Layer Security – newer, stronger version of SSL. |
| **HTTPS** | HTTP + SSL/TLS – secure web browsing (the padlock in your browser). |
| **SSH** | Secure Shell – secure remote login to servers (like a safe command line). |
| **Kerberos** | Strong authentication for client-server apps (uses secret-key cryptography). |

---

### 3. Management Protocols (Monitoring & Maintenance)

| Protocol | What it does |
|----------|--------------|
| **SNMP** | Simple Network Management Protocol – collects data from network devices (switches, routers, printers) for monitoring. |
| **ICMP** | Internet Control Message Protocol – sends error messages and operational info (e.g., "host unreachable"). Used by `ping`. |

---

## Ports (The Doors to Your Computer)

- A **port** is like an apartment number – IP address is the building, port is the specific door.
- Range: **0–65535**
- **Well-known ports (0–1023):** Reserved for common services.

### Common Ports to Memorize
| Port | Protocol/Service |
|------|------------------|
| 20 | FTP (data transfer) |
| 21 | FTP (command control) |
| 22 | SSH (secure shell) |
| 23 | Telnet (old, insecure remote login) |
| 25 | SMTP (sending email) |
| 53 | DNS (domain name system) |
| 80 | HTTP (web) |
| 110 | POP3 (receiving email) |
| 123 | NTP (network time protocol) |
| 143 | IMAP (email management) |
| 161 | SNMP (network monitoring) |
| 443 | HTTPS (secure web) |

---

## Internet Protocol Suite (TCP/IP Model)

The **TCP/IP model** has 4 layers. Each layer has a job:

| Layer | What it does | Protocols Used |
|-------|--------------|----------------|
| **Application** | Handles user-facing apps (email, web browsing) | HTTP, HTTPS, FTP, SMTP, POP3, IMAP, DNS |
| **Transport** | Manages communication between devices | TCP (reliable), UDP (fast) |
| **Internet** | Handles addressing and routing | IP, ICMP, IPsec |
| **Network Access** | Physical transmission of data (cables, Wi-Fi) | Ethernet, MAC, ARP, DSL |

> 💡 **Note:** The OSI model has 7 layers, but TCP/IP's 4-layer model is simpler and more practical.

---

## Azure Monitoring Tools

| Tool | What it does |
|------|--------------|
| **Network Watcher** | Capture packet data, troubleshoot network issues in Azure. |
| **Network Performance Monitor** | Monitor health and performance of networks (cloud + on-premises). |
| **Performance Monitor** | Tracks network connectivity, finds slow segments, monitors routes. |
<<<<<<< HEAD



# NEW TOPIC:
# IP Address Standards and Services – Simple Notes

## ARP (Address Resolution Protocol)
- **Job:** Finds the MAC address of a device when you know its IP address.
- Think of it like: You have someone's house number (IP), but you need their fingerprint (MAC) to identify them.
- **RARP (Reverse ARP):** Does the opposite – finds IP address if you know the MAC.
- **For IPv6:** ARP is replaced by **NDP (Neighbor Discovery Protocol)**.

---

## TCP/IP Model (Quick Refresher)
TCP/IP has 4 layers. Each layer has a job:

| Layer | What it does | Protocols Used |
|-------|--------------|----------------|
| **Application** | Handles user apps (browsers, email) | HTTP, HTTPS, DNS, FTP, SMTP, POP3, IMAP, SSH, TLS/SSL |
| **Transport** | Splits data into chunks, assigns ports | TCP (reliable), UDP (fast) |
| **Internet** | Adds IP addresses, routes packets | IP, IPv4, IPv6, ICMP, IPsec |
| **Network Access** | Physical transmission (cables, Wi-Fi) | ARP, MAC, Ethernet, DSL, ISDN |

> 💡 **Key Point:** TCP/IP is **open standard** – no single company owns it, so it works with everything.

---

## IPv4 (Internet Protocol version 4)
- Released: **1983**
- Address size: **32 bits**
- Total possible addresses: **4.3 billion**
- Format: **Dotted-decimal** (e.g., `192.168.0.1`)

### Parts of an IPv4 Address
- **Network part:** Identifies the network (first part of the address)
- **Host part:** Identifies the specific device (last part)

Example: `192.168.0.1`
- Network part: `192.168.0`
- Host part: `1`

### IPv4 Address Classes
| Class | Start | End | Subnet Mask | Use |
|-------|-------|-----|-------------|-----|
| A | 0.0.0.0 | 127.255.255.255 | 255.0.0.0 | Large networks |
| B | 128.0.0.0 | 191.255.255.255 | 255.255.0.0 | Medium networks |
| C | 192.0.0.0 | 223.255.255.255 | 255.255.255.0 | Small networks |
| D | 224.0.0.0 | 239.255.255.255 | – | Multicast (one-to-many) |
| E | 240.0.0.0 | 255.255.255.255 | – | Reserved (experimental) |

---

## Subnetting (Dividing Networks)
- **Subnet:** A smaller network inside a larger network.
- **Subnet Mask:** Tells you which part of the IP is the network and which part is the host.

### Example
IP: `192.168.0.1`  
Subnet Mask: `255.255.255.0`  
- The `255` parts are **fixed** (network part = `192.168.0`)  
- The `0` part is **flexible** (host part can be `1` to `254`)

### CIDR Notation (Simpler Way)
Instead of writing `255.255.255.0`, you write: `192.168.0.0/24`  
- `/24` means **24 bits are fixed** for the network, **8 bits** are for hosts.
- `/24` = 256 addresses (254 usable – 1 for network, 1 for broadcast)

Common CIDR blocks:
- `/24` = 256 addresses
- `/16` = 65,536 addresses
- `/8` = 16.7 million addresses

---

## Private IP Addresses (Not on the Internet)
These IPs are for **internal use only** – routers on the internet ignore them.

| Name | CIDR | Address Range | Use |
|------|------|---------------|-----|
| 24-bit block | 10.0.0.0/8 | 10.0.0.0 – 10.255.255.255 | Large private networks |
| 20-bit block | 172.16.0.0/12 | 172.16.0.0 – 172.31.255.255 | Medium networks |
| 16-bit block | 192.168.0.0/16 | 192.168.0.0 – 192.168.255.255 | Home/small office |

> 💡 **NAT (Network Address Translation):** Lets multiple private devices share one public IP to access the internet.

---

## Special-Use Addresses (You'll See These)
| Address Range | What it's for |
|---------------|---------------|
| 127.0.0.0 – 127.255.255.255 | **Loopback** – your own computer (localhost) |
| 169.254.0.0 – 169.254.255.255 | **APIPA** – when DHCP fails, Windows auto-assigns this |
| 255.255.255.255 | **Broadcast** – sends to all devices on network |

---

## IPv4 Address Exhaustion (We Ran Out!)
- Too many devices, not enough IPv4 addresses.
- Solutions:
  - **NAT** (one public IP for many private devices)
  - **CIDR** (more efficient use of address space)
  - **IPv6** (long-term fix)

---

## IPv6 (Internet Protocol version 6)
- Released: **2006** (commercially)
- Address size: **128 bits**
- Total addresses: **340 undecillion** (way more than we'll ever need)
- Format: **8 groups of hexadecimal** separated by colons

### Example IPv6 Address
Full: `2001:0db8:0000:0000:0000:8a2e:0370:7334`  
Shortened: `2001:db8::8a2e:370:7334`

### Shortening Rules
1. Remove **leading zeros** in a group (0042 → 42)
2. Replace **consecutive zero groups** with `::` (can use only once)

### IPv6 Benefits
- **Built-in security** (IPsec is mandatory)
- **Autoconfiguration** – devices can assign themselves an IP
- **No NAT needed** – true end-to-end connectivity
- **Multicast & Anycast** – better broadcasting options

---

## DNS (Domain Name System)
- **Job:** Translates human-friendly names (like `google.com`) into IP addresses (like `142.250.80.46`).
- Think of it as the **phonebook of the internet**.

### How DNS Works
1. You type `google.com` in browser.
2. Your computer asks a DNS server: "What's the IP for google.com?"
3. DNS server checks its cache. If not there, it asks other DNS servers.
4. Finally finds the IP and sends it back.
5. Your browser connects to that IP.

### DNS Record Types
| Record | What it does |
|--------|--------------|
| **A** | Maps domain to IPv4 address |
| **AAAA** | Maps domain to IPv6 address |
| **CNAME** | Alias (e.g., `www` → `domain.com`) |
| **MX** | Mail server for the domain |
| **NS** | Name servers for the domain |
| **SOA** | Start of Authority – main info about the domain |

---

## What Azure Offers

### Azure DNS
- Host your domain's DNS records in Azure.
- Manage A, AAAA, CNAME, MX, NS, SOA records.
- **Alias records:** Point to Azure resources directly (like load balancers, CDN).

> Note: Azure DNS is for **hosting** DNS – you still need a **registrar** (like GoDaddy) to buy the domain name.

### Azure Virtual Network
- Build your own private network in the cloud.
- Use **private IP addresses** (like 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16).
- Create **subnets** to organize resources.
- Connect to on-premises networks via VPN or ExpressRoute.

---

## Quick Summary Table

| Concept | What It Is |
|---------|------------|
| **ARP** | Finds MAC address from IP |
| **IPv4** | 32-bit addresses (e.g., 192.168.1.1) – running out |
| **IPv6** | 128-bit addresses (e.g., 2001:db8::1) – future-proof |
| **Subnet** | Divides a network into smaller pieces |
| **CIDR** | Shorthand for subnet masks (/24, /16, etc.) |
| **Private IP** | Internal use only (10.x, 172.16–31.x, 192.168.x) |
| **NAT** | Lets private IPs share one public IP |
| **DNS** | Translates domain names to IP addresses |



# Summary

## What We Learned This Week

### Networks Are Made of Two Things:
1. **Tangible stuff** (hardware):
   - Network devices (switches, routers, hubs, repeaters)
   - Cables and physical connections

2. **Intangible stuff** (software/rules):
   - Network protocols (TCP/IP, HTTP, DNS, etc.)
   - Security protocols (SSL/TLS, SSH, HTTPS)
   - IP addressing (IPv4, IPv6)

---

## Why This Matters
- Understanding how networks work is **essential** before learning Azure cloud.
- The same principles apply to:
  - Your home Wi-Fi
  - A company's office network
  - The entire internet
  - Microsoft Azure cloud networks

---

## Key Takeaways

### Network Types
| Type | What It Covers |
|------|----------------|
| **PAN** | Personal devices (phone ↔ smartwatch) |
| **LAN** | One building (office, school, home) |
| **MAN** | City-wide connections |
| **WAN** | Connects different cities/countries |

### Network Topologies (Layouts)
- **Bus:** One cable, all devices connected (simple but fragile)
- **Ring:** Devices connected in a circle
- **Star:** All devices connect to a central switch (most common)
- **Mesh:** Multiple connections for reliability

### Network Devices
| Device | Job |
|--------|-----|
| **Repeater** | Boosts signal for longer distances |
| **Hub** | Connects devices but sends data to everyone (old tech) |
| **Switch** | Connects devices intelligently (sends data only to right device) |
| **Router** | Connects different networks (like your home network to the internet) |
| **Access Point** | Provides Wi-Fi |

### Protocols (The Rules)
- **TCP/IP:** The foundation of internet communication
- **HTTP/HTTPS:** Web browsing
- **DNS:** Translates google.com to IP addresses
- **DHCP:** Automatically assigns IP addresses to devices
- **SMTP/POP3/IMAP:** Email sending/receiving
- **SSH:** Secure remote access to servers

### IP Addressing
- **IPv4:** 32-bit addresses (e.g., 192.168.1.1) – we're running out!
- **IPv6:** 128-bit addresses (e.g., 2001:db8::1) – future-proof, massive number of addresses
- **Private IPs:** Used inside networks (10.x, 172.16–31.x, 192.168.x)
- **Public IPs:** Visible on the internet
- **NAT:** Lets many private IPs share one public IP

### Subnetting
- Dividing a big network into smaller pieces
- **CIDR notation:** /24, /16, /8 (shows how many IPs are in the network)

### DNS (Domain Name System)
- The **phonebook of the internet**
- Converts human-friendly names (google.com) to computer-friendly IPs (142.250.80.46)

---

## Why This Helps with Azure
- Azure Virtual Networks work exactly like physical networks – just in the cloud.
- You'll use the same concepts:
  - IP addressing
  - Subnets
  - DNS
  - Routing
  - Firewalls (NSGs)
- Azure just makes it **software-defined** so you can configure it with clicks or code.
=======
<<<<<<< HEAD





```markdown
## Networking Commands – Simple Notes from My Terminal

**Where:** GitHub Codespaces (Ubuntu Linux)  
---

### 1. `ip addr` – See my network cards and IP addresses
**What it does:** Shows all network interfaces (like Wi-Fi, Ethernet, virtual) and their IP addresses.

**My output:**
```
1: lo: <LOOPBACK,UP,LOWER_UP> ... inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> ... inet 10.0.1.14/16 brd 10.0.255.255 scope global eth0
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> ... inet 172.17.0.1/16 scope global docker0
```
**What it means:**
- `lo` = loopback – your computer talking to itself (localhost).
- `eth0` = my main network card, IP `10.0.1.14` with a subnet mask of `255.255.0.0` (/16).
- `docker0` = a virtual network for Docker (not being used right now).

---

### 2. `ping` – Test if a computer is reachable (like a knock on the door)
**What it does:** Sends a small packet and waits for an answer. It uses a protocol called ICMP.

#### a) `ping 4 8.8.8.8` – I made a typo here
**Output:**
```
47 packets transmitted, 0 received, 100% packet loss
```
**What happened:** I typed `4` instead of `-c 4`, so it kept pinging forever until I pressed Ctrl+C. All packets were lost.

#### b) `ping -c 4 8.8.8.8` – Send only 4 pings to Google's DNS (8.8.8.8)
**Output:**
```
4 packets transmitted, 0 received, 100% packet loss
```
**Why?** In Codespaces, ICMP is blocked for security. So even though the internet works, `ping` won't get replies.

#### c) `ping -c 2 google.com` – Ping Google by name
**Output:**
```
PING google.com (142.250.207.206) ... 2 packets transmitted, 0 received
```
**What it means:** DNS worked – it found Google's IP `142.250.207.206`. But still no ping replies (ICMP blocked).

**Simple lesson:** Don't rely on `ping` in cloud environments. Use `curl` or `wget` instead.

---

### 3. `apt` – The app store for Ubuntu (install/update software)

#### a) `sudo apt --upgrade` – Wrong command, showed help instead
**Output:** (help text)  
**Lesson:** To upgrade packages, use `sudo apt upgrade`.

#### b) `sudo apt install --upgrade` – Still wrong, did nothing
**Output:** `0 upgraded, 0 newly installed`  
**Lesson:** `--upgrade` is not a valid option for `install`.

#### c) `sudo apt get --upgrade` – Another mistake
**Output:** `E: Invalid operation get`  
**Lesson:** The correct command is `apt-get` or `apt`.

#### d) `sudo apt install -y traceroute` – Installs the traceroute tool
**Output:** (lots of download and installation messages)  
**Lesson:** Now I have `traceroute` available.

#### e) `sudo apt install -y netcat` – Tried to install netcat
**Output:** Said `netcat` is a "virtual package" and I need to choose `netcat-openbsd` or `netcat-traditional`.  
**Lesson:** Some packages are just placeholders; you must pick the real one.

#### f) `sudo apt update && sudo apt install -y dnsutils net-tools iputils-ping traceroute curl wget tcpdump nmap netcat-openbsd telnet mtr whois` – The big install
**Output:** (long list of installed packages)  
**Lesson:** This installed a full set of networking tools all at once. Now I have `dig`, `nslookup`, `ifconfig`, `tcpdump`, `nmap`, `nc`, `telnet`, `mtr`, `whois`, and more.

---

### 4. `curl -I https://www.google.com` – Check if a website is reachable
**What it does:** Fetches just the headers (not the whole page) from Google using HTTPS (port 443).

**Output:**
```
HTTP/2 200 
content-type: text/html; charset=ISO-8859-1
...
```
**What it means:** `200 OK` means Google is alive and my internet works! This proves that although `ping` fails, web traffic is fine.

---

### 5. `traceroute` – See the path my packets take to a destination

#### Before install: `traceroute 8.8.8.8`
**Output:** `bash: traceroute: command not found`  
**Lesson:** Tool wasn't installed yet.

#### After install: `traceroute 8.8.8.8`
**Output:**
```
1  * * *
2  * * *
3  * * *
... (all stars)
```
**Why?** `traceroute` also uses ICMP or UDP, which are blocked. No replies.

#### `sudo tcptraceroute 8.8.8.8 443` – Try TCP version on port 443
**Output:** Still all stars. Even TCP traceroute may be blocked.

**Lesson:** In some cloud environments, you can't trace the route.

---

### 6. `ip route` – Show the routing table (how my computer sends packets)
**What it does:** Lists rules for where to send data.

**Output:**
```
default via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14 metric 100
10.0.0.0/16 dev eth0 proto kernel scope link src 10.0.1.14
168.63.129.16 via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14
169.254.169.254 via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
```
**What it means:**
- `default via 10.0.0.1` = all internet traffic goes through the router at `10.0.0.1`.
- `10.0.0.0/16` = my local network (all devices with IPs starting with 10.0).
- `168.63.129.16` and `169.254.169.254` are special Azure services (metadata and DNS).
- `172.17.0.0/16` = Docker's private network (not active now).

---

### 7. `wget -O /dev/null http://google.com` – Download a webpage without saving it
**What it does:** Connects to Google over HTTP (port 80) and downloads the page but throws it away (`-O /dev/null`). It shows if the connection works.

**Output:**
```
--2026-02-25 ... http://google.com/ ... 200 OK ... saved [20014]
```
**What it means:** `200 OK` means HTTP works fine. Google redirected to `www.google.com` but still returned success.

**Lesson:** Use `wget` or `curl` to test web connectivity when `ping` fails.

---

### 8. `dig` – DNS lookup (find IP address of a domain)

#### Before install: `dig google.com`
**Output:** `bash: dig: command not found`

#### After install: `sudo dig google.com`
**Output:**
```
;; ANSWER SECTION:
google.com. 138 IN A 142.250.206.110
```
**What it means:** DNS is working! Google's domain name resolves to IP `142.250.206.110`.

---

### 9. `netstat -an` – Show all network connections and listening ports
**What it does:** Lists every open port and active connection on my machine.

**Output (shortened):**
```
Active Internet connections
tcp  0  0 127.0.0.53:53   0.0.0.0:*   LISTEN      (DNS server)
tcp  0  0 10.0.1.14:43204 20.60.84.33:443 ESTABLISHED (outgoing HTTPS)
tcp  0  0 0.0.0.0:2222    0.0.0.0:*   LISTEN      (Codespaces SSH)
```
**What it means:**
- `LISTEN` = my computer is waiting for someone to connect (like a web server or SSH).
- `ESTABLISHED` = an active connection to another computer (here, to GitHub on port 443).
- Port `53` (DNS) is listening locally.
- Port `2222` is for Codespaces SSH.

---

### 🔍 Simple Key Takeaways
- **ICMP is blocked** in Codespaces – `ping` and `traceroute` won't work. Don't panic; use `curl` or `wget` to test internet.
- **Install tools first** – many commands aren't pre-installed. Use `sudo apt install` to get them.
- **`curl -I` or `wget`** are your friends for checking web access.
- **`ip addr`** shows your IP.
- **`ip route`** shows your gateway.
- **`dig`** checks DNS.
- **`netstat -an`** shows open ports and active connections – great for security.

```
=======
# Networking Fundamentals

## 1. TCP/IP Model vs OSI Model
- **TCP/IP Model** (4 layers):
  1. **Application Layer** – protocols like HTTP, DNS, SSH
  2. **Transport Layer** – TCP (reliable, connection-oriented) and UDP (fast, connectionless)
  3. **Internet Layer** – handles IP addresses and routing (e.g., IPv4, IPv6)
  4. **Network Access Layer** – physical hardware and data link

- **OSI Model** (7 layers) – conceptual, not used as directly in practice:
  - Physical, Data Link, Network, Transport, Session, Presentation, Application

**Key takeaway:** Focus on TCP/IP layers – they map directly to how the internet works.

---

## 2. DNS (Domain Name System)
- Translates human-friendly domain names (e.g., `google.com`) into machine‑readable IP addresses (e.g., `142.250.80.46`).
- **How it works:** Your computer asks a DNS server, “What is the IP of google.com?” The DNS server replies with the IP, then your browser connects to that IP.
- If DNS fails, websites won’t open by name, but you can still access them by typing the IP address directly.

---

## 3. Ports
- Think of an **IP address** like a building address, and **ports** like apartment numbers inside that building.
- Common ports:
  - **22** – SSH (secure remote terminal)
  - **53** – DNS
  - **80** – HTTP (unencrypted web traffic)
  - **443** – HTTPS (encrypted web traffic)
  - **3389** – RDP (Remote Desktop Protocol for Windows)
  - **25** – SMTP (email sending)

---

## 4. Private vs Public IP Addresses
- **Private IPs** – used inside your home or office network (e.g., `192.168.1.x`, `10.0.0.x`). They are not routable on the public internet.
- **Public IP** – assigned to your router by your ISP; this is the address the internet sees.
- **NAT (Network Address Translation)** – the router translates private IPs to its public IP so multiple devices can share one public IP.

---

## 5. Subnets and CIDR Notation
- A **subnet** divides a network into smaller, manageable pieces.
- **CIDR notation** (e.g., `/24`) indicates how many IP addresses are in the subnet:
  - `/24` → 256 addresses total, 254 usable (first is network, last is broadcast)
  - `/16` → 65,536 addresses
- Used heavily when designing Azure VNets and on‑prem networks.

---

## 6. DHCP (Dynamic Host Configuration Protocol)
- Automatically assigns IP addresses, subnet masks, default gateway, and DNS servers to devices when they join a network.
- If DHCP fails, Windows devices may assign themselves an **APIPA** address (`169.254.x.x`), meaning they couldn’t reach a DHCP server.





```markdown
## Networking Commands – Simple Notes from My Terminal

**Where:** GitHub Codespaces (Ubuntu Linux)  
---

### 1. `ip addr` – See my network cards and IP addresses
**What it does:** Shows all network interfaces (like Wi-Fi, Ethernet, virtual) and their IP addresses.

**My output:**
```
1: lo: <LOOPBACK,UP,LOWER_UP> ... inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> ... inet 10.0.1.14/16 brd 10.0.255.255 scope global eth0
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> ... inet 172.17.0.1/16 scope global docker0
```
**What it means:**
- `lo` = loopback – your computer talking to itself (localhost).
- `eth0` = my main network card, IP `10.0.1.14` with a subnet mask of `255.255.0.0` (/16).
- `docker0` = a virtual network for Docker (not being used right now).

---

### 2. `ping` – Test if a computer is reachable (like a knock on the door)
**What it does:** Sends a small packet and waits for an answer. It uses a protocol called ICMP.

#### a) `ping 4 8.8.8.8` – I made a typo here
**Output:**
```
47 packets transmitted, 0 received, 100% packet loss
```
**What happened:** I typed `4` instead of `-c 4`, so it kept pinging forever until I pressed Ctrl+C. All packets were lost.

#### b) `ping -c 4 8.8.8.8` – Send only 4 pings to Google's DNS (8.8.8.8)
**Output:**
```
4 packets transmitted, 0 received, 100% packet loss
```
**Why?** In Codespaces, ICMP is blocked for security. So even though the internet works, `ping` won't get replies.

#### c) `ping -c 2 google.com` – Ping Google by name
**Output:**
```
PING google.com (142.250.207.206) ... 2 packets transmitted, 0 received
```
**What it means:** DNS worked – it found Google's IP `142.250.207.206`. But still no ping replies (ICMP blocked).

**Simple lesson:** Don't rely on `ping` in cloud environments. Use `curl` or `wget` instead.

---

### 3. `apt` – The app store for Ubuntu (install/update software)

#### a) `sudo apt --upgrade` – Wrong command, showed help instead
**Output:** (help text)  
**Lesson:** To upgrade packages, use `sudo apt upgrade`.

#### b) `sudo apt install --upgrade` – Still wrong, did nothing
**Output:** `0 upgraded, 0 newly installed`  
**Lesson:** `--upgrade` is not a valid option for `install`.

#### c) `sudo apt get --upgrade` – Another mistake
**Output:** `E: Invalid operation get`  
**Lesson:** The correct command is `apt-get` or `apt`.

#### d) `sudo apt install -y traceroute` – Installs the traceroute tool
**Output:** (lots of download and installation messages)  
**Lesson:** Now I have `traceroute` available.

#### e) `sudo apt install -y netcat` – Tried to install netcat
**Output:** Said `netcat` is a "virtual package" and I need to choose `netcat-openbsd` or `netcat-traditional`.  
**Lesson:** Some packages are just placeholders; you must pick the real one.

#### f) `sudo apt update && sudo apt install -y dnsutils net-tools iputils-ping traceroute curl wget tcpdump nmap netcat-openbsd telnet mtr whois` – The big install
**Output:** (long list of installed packages)  
**Lesson:** This installed a full set of networking tools all at once. Now I have `dig`, `nslookup`, `ifconfig`, `tcpdump`, `nmap`, `nc`, `telnet`, `mtr`, `whois`, and more.

---

### 4. `curl -I https://www.google.com` – Check if a website is reachable
**What it does:** Fetches just the headers (not the whole page) from Google using HTTPS (port 443).

**Output:**
```
HTTP/2 200 
content-type: text/html; charset=ISO-8859-1
...
```
**What it means:** `200 OK` means Google is alive and my internet works! This proves that although `ping` fails, web traffic is fine.

---

### 5. `traceroute` – See the path my packets take to a destination

#### Before install: `traceroute 8.8.8.8`
**Output:** `bash: traceroute: command not found`  
**Lesson:** Tool wasn't installed yet.

#### After install: `traceroute 8.8.8.8`
**Output:**
```
1  * * *
2  * * *
3  * * *
... (all stars)
```
**Why?** `traceroute` also uses ICMP or UDP, which are blocked. No replies.

#### `sudo tcptraceroute 8.8.8.8 443` – Try TCP version on port 443
**Output:** Still all stars. Even TCP traceroute may be blocked.

**Lesson:** In some cloud environments, you can't trace the route.

---

### 6. `ip route` – Show the routing table (how my computer sends packets)
**What it does:** Lists rules for where to send data.

**Output:**
```
default via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14 metric 100
10.0.0.0/16 dev eth0 proto kernel scope link src 10.0.1.14
168.63.129.16 via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14
169.254.169.254 via 10.0.0.1 dev eth0 proto dhcp src 10.0.1.14
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
```
**What it means:**
- `default via 10.0.0.1` = all internet traffic goes through the router at `10.0.0.1`.
- `10.0.0.0/16` = my local network (all devices with IPs starting with 10.0).
- `168.63.129.16` and `169.254.169.254` are special Azure services (metadata and DNS).
- `172.17.0.0/16` = Docker's private network (not active now).

---

### 7. `wget -O /dev/null http://google.com` – Download a webpage without saving it
**What it does:** Connects to Google over HTTP (port 80) and downloads the page but throws it away (`-O /dev/null`). It shows if the connection works.

**Output:**
```
--2026-02-25 ... http://google.com/ ... 200 OK ... saved [20014]
```
**What it means:** `200 OK` means HTTP works fine. Google redirected to `www.google.com` but still returned success.

**Lesson:** Use `wget` or `curl` to test web connectivity when `ping` fails.

---

### 8. `dig` – DNS lookup (find IP address of a domain)

#### Before install: `dig google.com`
**Output:** `bash: dig: command not found`

#### After install: `sudo dig google.com`
**Output:**
```
;; ANSWER SECTION:
google.com. 138 IN A 142.250.206.110
```
**What it means:** DNS is working! Google's domain name resolves to IP `142.250.206.110`.

---

### 9. `netstat -an` – Show all network connections and listening ports
**What it does:** Lists every open port and active connection on my machine.

**Output (shortened):**
```
Active Internet connections
tcp  0  0 127.0.0.53:53   0.0.0.0:*   LISTEN      (DNS server)
tcp  0  0 10.0.1.14:43204 20.60.84.33:443 ESTABLISHED (outgoing HTTPS)
tcp  0  0 0.0.0.0:2222    0.0.0.0:*   LISTEN      (Codespaces SSH)
```
**What it means:**
- `LISTEN` = my computer is waiting for someone to connect (like a web server or SSH).
- `ESTABLISHED` = an active connection to another computer (here, to GitHub on port 443).
- Port `53` (DNS) is listening locally.
- Port `2222` is for Codespaces SSH.

---

### 🔍 Simple Key Takeaways
- **ICMP is blocked** in Codespaces – `ping` and `traceroute` won't work. Don't panic; use `curl` or `wget` to test internet.
- **Install tools first** – many commands aren't pre-installed. Use `sudo apt install` to get them.
- **`curl -I` or `wget`** are your friends for checking web access.
- **`ip addr`** shows your IP.
- **`ip route`** shows your gateway.
- **`dig`** checks DNS.
- **`netstat -an`** shows open ports and active connections – great for security.

```
