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