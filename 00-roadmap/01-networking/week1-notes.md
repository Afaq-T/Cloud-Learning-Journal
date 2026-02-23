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