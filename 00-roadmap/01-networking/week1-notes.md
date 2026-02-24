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


NEW TOPIC:
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


NEW TOPIC:
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