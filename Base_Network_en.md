[Fa](https://github.com/ussefT/Essential/blob/main/Base_Network_fa.md)
# Linux Networking Notes

## Set IP for Interface in Linux

```bash
ip addr show
```

See all interfaces on the OS:

```bash
ip addr show
```

Set an IP address for an interface:

```bash
ip addr add 192.168.56.11/24 dev enp0s8
```

### What does `/24` mean?

`/24` means **24 bits are used for the Network part** and **8 bits are used for the Host part**.

Example:

```text
192.168.56.11/24

Netmask: 255.255.255.0
Network: 192.168.56.0
Host:    11
```

> In short: `Netmask = 255.255.255.0` tells which part of the IP belongs to the Network and which part belongs to the Host.

---

## What is Ping?

`ping` is a network tool used to test whether a system can reach another IP address or host.

Example:

```bash
ping 192.168.1.10
```

In IPv4, `ping` normally uses **ICMP Echo Request**, and the destination replies with an **ICMP Echo Reply** when reachable.

---

## 3 Devices Connected to a Switch

Assume 3 devices are connected to a Switch.

When:

> Device A → ping → Device B

and the ping works, how does the Switch work?

### How does a Switch work with IP if it works with MAC addresses?

A Switch works at the **Data Link Layer (Layer 2)** and uses **MAC addresses** to forward Ethernet frames.

A Switch has a table called the **CAM Table (Content Addressable Memory)**.

Example:

```text
MAC Address          Port
AA:AA:AA:AA:AA:01    Port 1
BB:BB:BB:BB:BB:02    Port 2
CC:CC:CC:CC:CC:03    Port 3
```

When a frame enters a Switch for the first time, the Switch can learn the **Source MAC Address** and the port on which the frame arrived, then store that information in the CAM Table.

If the destination MAC is unknown, the Switch **floods** the frame to the other ports.

After the MAC address is learned, the Switch can send the frame only to the correct destination port.

---

## How Does the OS Know Which MAC Belongs to an IP?

The operating system uses **ARP (Address Resolution Protocol)** to find the MAC address associated with an IPv4 address.

### ARP

ARP is used to discover:

```text
IP Address → MAC Address
```

Example:

```text
Who has 192.168.1.20?
Tell 192.168.1.10
```

The device that owns `192.168.1.20` replies with its MAC address.

On modern Linux systems, you can inspect the neighbor/ARP table with:

```bash
ip neigh
```

On systems that have the older `arp` tool installed:

```bash
arp -n
```

To remove an entry:

```bash
sudo arp -d 192.168.1.20
```

Modern alternative:

```bash
sudo ip neigh del 192.168.1.20 dev eth0
```

When the first ping is sent, ARP may happen first and the result can be stored in the ARP/neighbor cache.

---

## Switch Can Have a Loop

Yes. If redundant Layer 2 paths exist between switches, a **Layer 2 loop** can occur.

A loop can cause:

- Broadcast Storm
- Duplicate Frames
- MAC Table Instability

Protocols such as **STP (Spanning Tree Protocol)** are used to prevent these problems.

---

# OSI Layers

The OSI model has 7 layers:

| Layer | Name |
|---:|---|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

Examples:

```text
Layer 7 → HTTP, DNS, SSH
Layer 4 → TCP, UDP
Layer 3 → IP, ICMP
Layer 2 → Ethernet, MAC, ARP
Layer 1 → Cable, Fiber, Radio
```

---

# DHCP

**DHCP (Dynamic Host Configuration Protocol)** can automatically assign an IP address to a device.

DHCP normally uses these ports:

```text
Server → UDP 67
Client → UDP 68
```

So:

```text
Client source port:      68
Server destination port: 67
```

### DHCP Discover

At the beginning, the Client does not have an IP address yet, so it can use:

```text
Source IP:      0.0.0.0
Destination IP: 255.255.255.255
```

The normal DHCP process is:

```text
DHCP Discover
       ↓
DHCP Offer
       ↓
DHCP Request
       ↓
DHCP ACK
```

### What is DHCP ACK?

**DHCP ACK (Acknowledgement)** is the confirmation message from the DHCP Server.

At this stage, the Server confirms the requested configuration. It can include:

```text
IP Address
Netmask
Default Gateway
DNS Server
Lease Time
```

Simply:

```text
Offer   → Server offers an IP
Request → Client requests that IP
ACK     → Server confirms the request
```

---

## Install / Search DHCP Server Package

Search for the package:

```bash
apt search isc-dhcp-server
```

> The original text had `dehcp-server`; the common package name on Debian/Ubuntu is `isc-dhcp-server`.

### DHCP Configuration

On Debian/Ubuntu, the main ISC DHCP Server configuration file is usually:

```text
/etc/dhcp/dhcpd.conf
```

For example, you can configure a domain name:

```conf
option domain-name "HI";
```

You can also define a subnet:

```conf
subnet 192.168.1.0 netmask 255.255.255.0 {
}
```

After changing the configuration:

```bash
sudo systemctl restart isc-dhcp-server
```

### Example

Devices are connected to a Switch, and one device runs `isc-dhcp-server`. The DHCP Server can then provide IP addresses and other network settings automatically to the other devices.

---

## DHCP Client

Release the current IP:

```bash
sudo dhclient -r eth0
```

Request an IP automatically:

```bash
sudo dhclient eth0
```

---

## Important: DHCP Uses Broadcast

At the beginning of DHCP, the Client does not have a normal IP address yet and uses Broadcast to find a DHCP Server.

Therefore, the first DHCP messages can be sent to all devices in the Broadcast Domain.

> If the network or IP configuration is incorrect, DHCP may not work correctly.

---

# What is Netmask & Host?

For example:

```text
IP:      192.168.1.0/24
Netmask: 255.255.255.0
```

With `/24`:

```text
Network: 192.168.1
Host:    0 - 255
```

However, in a normal `192.168.1.0/24` subnet:

```text
Network Address:   192.168.1.0
Usable Hosts:      192.168.1.1 - 192.168.1.254
Broadcast Address: 192.168.1.255
```

---

# IP Range

In the old classful IPv4 model, IANA ranges were divided into Classes A, B, and C:

```text
Class A: 0.0.0.0     - 127.255.255.255
Class B: 128.0.0.0   - 191.255.255.255
Class C: 192.0.0.0   - 223.255.255.255
```

Today, **CIDR** and prefix lengths such as `/8`, `/16`, and `/24` are much more important than classful networking.

---

# Routing

When a system wants to send an IP packet, the Routing Table decides which path and interface should be used.

To add a specific route:

```bash
ip route add [specificIP]/24 dev enp0s4
```

Here, `[specificIP]` means a **Network Address**.

Example:

```bash
sudo ip route add 192.168.20.0/24 dev enp0s4
```

This route means that traffic for `192.168.20.0/24` should use interface `enp0s4`.

> Sending a packet to a Switch does not guarantee that the destination will reply. The destination must exist and an appropriate return path must also exist.

For another network:

```bash
ip route add [senderIP]/24 dev eth0
```

Example:

```bash
sudo ip route add 10.10.10.0/24 dev eth0
```

If the destination is not known by a more specific route, a Default Route can be used:

```bash
ip route add default dev eth0
```

In normal networks, the Default Route usually points to a Gateway:

```bash
sudo ip route add default via 192.168.1.1 dev eth0
```

---

# Router — Layer 3

A Router works mainly at **Layer 3 (Network Layer)** and works with IP addresses and routing tables.

### When a Device Connects to a Router

A Router has interfaces, and each interface can have an IP address.

Show interfaces:

```bash
ip addr show
```

Example:

```text
Router
 ├── eth0 → 192.168.1.1/24
 └── eth1 → 10.0.0.1/24
```

Each router interface normally has an IP address appropriate for the network connected to that interface.

---

# Give All Devices a Route

Show the Routing Table:

```bash
ip route
```

Example:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.50
```

---

## Example: `ping 8.8.8.8`

When we run:

```bash
ping 8.8.8.8
```

In simple terms:

1. The OS checks whether the destination is on the local Network.
2. It checks the Routing Table.
3. If there is no direct route to the destination, it checks the Default Route.
4. The packet is sent to the Gateway/Router.
5. The Router forwards the packet according to its Routing Table.

---

# Router Information

When opening the Router panel, we may see something like:

```text
IP Address:  192.168.1.50
Netmask:     255.255.255.0
Gateway:     192.168.1.1
```

Meaning:

```text
IP Address
→ The IP assigned to the device interface.

Netmask
→ Defines which part of the IP is Network and which part is Host.

Gateway
→ The device to which traffic outside the local network is normally sent.
```

---

# TTL

**TTL (Time To Live)** is a value in the IP header used to limit the number of router hops a packet can make.

Simply:

```text
Packet
  ↓
Router 1 → TTL - 1
  ↓
Router 2 → TTL - 1
  ↓
Router 3 → TTL - 1
```

If the TTL reaches `0`, the Router normally drops the packet and sends an ICMP **Time Exceeded** message.

---

## Traceroute

To see the path a packet takes:

```bash
traceroute 4.2.2.4
```

If the command is not installed:

```bash
sudo apt install traceroute
```

`traceroute` uses TTL changes and ICMP responses to reveal the hops on the path.

---

# Networking Questions

## Suppose two computers are connected to a switch and their NICs are configured with `150.70.10.10/8` and `150.90.4.1/8`. Can these computers ping each other, and why?

### Answer

Yes, both computers can ping each other.

Because:

```text
150.70.10.10/8
150.90.4.1/8
```

with `/8` use this Netmask:

```text
255.0.0.0
```

Therefore, the Network Address of both is:

```text
150.0.0.0/8
```

So both computers are on the **same network**, and because they are directly connected to the same **Switch**, they do not need a Router to communicate with each other.

Simple flow:

```text
PC A
150.70.10.10/8
   |
   | Ethernet / MAC
   v
 Switch
   ^
   | Ethernet / MAC
   |
PC B
150.90.4.1/8
```

Before sending the IP traffic, PC A can use ARP to discover the MAC address of `150.90.4.1` and then send the Ethernet frame to that destination MAC.

**Result: Yes, they can ping each other.**

---

## Should each network interface of the Router and Switch, from right to left, have an IP address or not?

### Answer

**Router: Yes, normally each Router interface used at Layer 3 for a network has an IP address.**

Example:

```text
Router
eth0 → 192.168.1.1/24
eth1 → 10.0.0.1/24
```

**Normal Layer 2 Switch: No, Switch ports do not need IP addresses for frame forwarding; they use MAC addresses.**

However, the Switch itself may have an IP address on a **Management Interface / SVI**.

Example:

```text
Switch
Port 1 → PC
Port 2 → PC
Port 3 → Router

Management IP → 192.168.1.2/24
```

So:

```text
Router Interface            → Has an IP
Switch Port                 → Normally has no IP
Switch Management Interface → Can have an IP
```

---

## How many bits does IPv4 have?

**32-bit**

Example:

```text
192.168.1.10
```

IPv4 has four octets, and each octet is 8 bits:

```text
8 + 8 + 8 + 8 = 32 bits
```

---

## How many bits does IPv6 have?

**128-bit**

Example:

```text
2001:db8::1
```

IPv6 has 128 bits.
---
# Linux Networking Notes

## Assigning an IP Address to a Network Interface

Show all network interfaces and their IP addresses:

```bash
ip addr show  # Display all network interfaces on the operating system
```

Assign an IP address to an interface:

```bash
ip addr add 192.168.56.11/24 dev enp0s8
```

### What does `/24` mean?

`/24` is CIDR notation. It means that 24 bits of the IP address identify the network. It corresponds to the subnet mask `255.255.255.0`. The subnet mask indicates which bits identify the network and which bits identify hosts.

### What is `ping`?

### Three Devices Connected to a Switch

If three devices are connected to a switch, Device A can ping Device B when the network settings allow them to communicate.

### How Can a Switch Work with IP Addresses if It Uses MAC Addresses at the Data Link Layer?

A switch forwards Ethernet frames using MAC addresses. It learns which MAC addresses are reachable through which switch ports and stores this information in its CAM (Content Addressable Memory) table.

When a frame arrives, the switch learns from its source MAC address. If the destination MAC address is known, the switch forwards the frame to the associated port. If the destination MAC address is unknown, the switch floods the frame to the other relevant ports so that it can reach the destination.

A computer uses ARP (Address Resolution Protocol) to find the MAC address associated with an IPv4 address. ARP helps the operating system map an IP address to a MAC address.

Delete an ARP entry:

```bash
sudo arp -d ip  # Remove the IP-to-MAC address entry
```

The computer may save the learned IP-to-MAC mapping in its ARP cache after communication begins.

A router routes traffic using IP addresses.

### Can a Switch Create a Loop?

### OSI Layers

## DHCP

DHCP (Dynamic Host Configuration Protocol) automatically provides network settings, such as IP addresses, to devices. A DHCP server listens on UDP port `67`, while a DHCP client typically uses UDP port `68`.

A common DHCP exchange consists of these messages:

1. **Discover** — the client searches for a DHCP server.
2. **Offer** — the server offers an IP address and other settings.
3. **Request** — the client requests the offered configuration.
4. **ACK** — the server acknowledges the request and confirms the configuration.

A DHCP client's initial broadcast can use the following addressing information:

```text
Source IP:      0.0.0.0
Destination IP: 255.255.255.255
UDP source port: 68
UDP destination port: 67
```

The server offers an IP address to the interface, and the client accepts the offer by sending a request. The server then acknowledges the request.

Search for a DHCP server package with APT:

```bash
apt search dhcp-server
```

DHCP configuration file noted in these notes:

`/etc/default/dhcp.conf`

For example, a configuration may include an option like this:

```text
option domain-name "HI"
```

A subnet can be configured like this:

```text
subnet 192.168.1.0 netmask 255.255.255.0 {

}
```

Restart the DHCP server service:

```bash
sudo systemctl restart isc-dhcp-server
```

If devices are connected to a switch and one of them runs an ISC DHCP server, that server can automatically assign IP addresses to the other devices, provided the network and server are configured correctly.

Release an IP address obtained through DHCP and request another one:

```bash
sudo dhclient -r eth0  # Release the DHCP-assigned IP address
sudo dhclient eth0     # Request an IP address automatically
```

**Important:** DHCP clients use broadcast messages to find a DHCP server and request network settings. If the DHCP server or network is configured incorrectly, the request may fail or the device may not receive a valid IP address.

## Netmask and Host Addresses

For example:

```text
Subnet mask: 255.255.255.0
CIDR prefix: /24
Network:     192.168.1.0/24
Host field:  0–255 in the last octet
```

For a `/24` network, the last octet is used for host addressing. The network address and broadcast address are reserved for those purposes.

## IPv4 Address Ranges

IPv4 addresses were historically grouped into classes. IANA coordinates global IP address allocation and related registries.

```text
Class A: 0.0.0.0   – 127.255.255.255
Class B: 128.0.0.0 – 191.255.255.255
Class C: 192.0.0.0 – 223.255.255.255
```

## Routing

When a computer needs to send a packet, it checks its routing table to determine where the packet should go.

Add a route for a specific IP range through a network interface:

```bash
ip route add [specificIP]/24 dev enp0s4
```

This route sends matching traffic through the switch-connected interface. The destination device or its network also needs a valid route for the reply to return to the sender. For example:

```bash
ip route add [senderIP]/24 dev eth0
```

If the destination is unknown to the more specific routes, a default route can be used:

```bash
ip route add default dev eth0  # Send traffic with no more specific route through eth0
```

### Router (Layer 3)

A router operates at Layer 3 of the OSI model and forwards traffic using IP addresses.

A router may also provide DHCP service and assign IP addresses to connected devices. Each router interface that participates in an IP network normally needs an IP address appropriate for that network.

Show the network interfaces and their addresses:

```bash
ip addr show
```

[Show an example of the default Linux interface and the interface connected to a router.]

### Show Routes for the Device

```bash
ip route  # Display the routing table, including the default route if configured
```

Test connectivity to an IP address:

```bash
ping 8.8.8.8
```

The basic process is:

1. The operating system checks where the destination IP address should be sent.
2. It looks at the routing table.
3. If a default route is configured, the operating system sends the packet to the default gateway (usually the router's IP address).
4. The router receives the packet and forwards it according to its own routing table.

You can open the router's IP address in a web browser to access its administration panel.

Example client network settings:

```text
IP address: 192.168.1.50       # IP address assigned through Wi-Fi
Netmask:    255.255.255.0 (/24)
Gateway:   192.168.1.1         # The router used as the default gateway
```

The default gateway is where a device sends packets when it has no more specific route for the destination.

### TTL and Traceroute

TTL means **Time to Live**. It limits how many router hops an IP packet can pass through before it is discarded.

Use `traceroute` to see the route toward an IP address:

```bash
traceroute 4.2.2.4
```

## Networking Questions

### Question 1: Can These Two Computers Ping Each Other?

Suppose the network interfaces of two computers are connected to a switch. Assign these IP addresses:

- Computer 1: `150.70.10.10/8`
- Computer 2: `150.90.4.1/8`

Can the computers ping each other, and why?

**Answer:** Both computers are in the same IP network when the `/8` prefix is used. Since they are connected directly to the same switch, they do not need a router to communicate with each other on that local network.

**Result: Yes, they can ping each other**, assuming their interfaces are active and no firewall or other configuration prevents the traffic.

### Question 2: Do Router and Switch Interfaces Need IP Addresses?

Should each interface on the router and switch, reading the numbered interfaces from right to left, have an IP address?

[Answer]

### Question 3: How Many Bits Are in an IPv4 Address?

An IPv4 address is **32 bits** long.

### Question 4: How Many Bits Are in an IPv6 Address?

An IPv6 address is **128 bits** long.

## Routing Protocols

- RIP (Routing Information Protocol)

Set a static IP address for the DHCP server.

## Example Network Topology

```text
                                  ┌──────────────┐
                                   │   Internet   │
                                   └──────┬───────┘
                                          │
                                         (1)
                                          │
                                   ┌──────▼───────┐
                                   │ Edge Router  │
                                   │ 1941 Router2 │
                                   └──────┬───────┘
                                          │
                                         (2)
                                          │
     ┌────────────────────────────────────▼───────────────────────────────────┐
     │                         Local Area Network                             │
     │                                                                        │
     │                          ┌──────────────┐                              │
     │                          │  2950T-24    │                              │
     │                          │    Switch    │                              │
     │                          └───┬───┬───┬──┘                              │
     │                              │   │   │   │                             │
     │                             (3) (4) (5) (6)                            │
     │                              │   │   │   │                             │
     │                     ┌────────┘   │   │   └────────┐                    │
     │                     │            │   │            │                    │
     │              ┌──────▼─────┐ ┌────▼───┐ ┌────▼───┐ ┌────▼───┐           │
     │              │ DHCP Server│ │  PC1   │ │  PC2   │ │  PC3   │           │
     │              └────────────┘ └────────┘ └────────┘ └────────┘           │
     │                                                                        │
     └────────────────────────────────────────────────────────────────────────┘
```

## Question 5: Which Interfaces Need Static IP Addresses?

Each number in the diagram refers to a network interface on a networking device or computer. Determine which interfaces must be assigned IP addresses manually and which can receive IP addresses from the DHCP server.

## Question 6: Choose IP Addresses for the Diagram

Find the **public** and **private IPv4 address ranges** and determine which IP address can be assigned to each numbered network interface so that the proposed network can be implemented completely.

**Note:** Assume that the IP range `192.168.0.0/16` cannot be used.

## Question 7: Can DHCP Always Assign the Same IP Address to One Computer?

Research how a DHCP server on a local network can always assign a particular IP address to a specific computer (for example, the company manager's computer). Explain your answer in one or two paragraphs.

---

## DNS

DNS (Domain Name System) translates domain names into IP addresses.

Before DNS was commonly used, host files could be used to map names to IP addresses. Example entries:

```text
google.com 89.36.44.98
site.com   192.168.56.11
```

On Linux, the hosts file is located at `/etc/hosts`.

Query a DNS server explicitly with `nslookup`:

```bash
nslookup google.com 4.2.2.2
```

Example output from `nslookup google.com`:

```text
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   google.com
Address: 216.239.38.120
Name:   google.com
Address: 2001:4860:4802:32::78
```

### Where Does Linux Send DNS Requests?

DNS resolver configuration is commonly found in `/etc/resolv.conf`.

DNS queries usually use UDP, although TCP is also used in some situations.

- `A` records map a name to an IPv4 address.
- `AAAA` records map a name to an IPv6 address.

## Troubleshooting Internet Connectivity on Linux

1. **Check network interfaces:**

   ```bash
   ip addr show
   ```

   - The loopback interface uses `127.0.0.1` to refer to the local computer itself.
   - Check the other network interfaces as well.

2. **Check the routing table:**

   ```bash
   ip route
   ```

   Review the available routes and the default route.

3. **Test connectivity to a domain name:**

   ```bash
   ping google.com
   ```

   This sends ICMP echo requests after the name has been resolved to an IP address.

4. **Trace the route to the destination:**

   ```bash
   traceroute google.com
   ```

   This helps show the route and the IP addresses of the hops along the way.

5. **Check the DNS server configuration:**

   Inspect `/etc/resolv.conf`.

6. **Inspect DNS records:**

   ```bash
   dig google.com
   ```

   This can show DNS records such as `A` and `AAAA` records.

7. **Watch the route in real time:**

   ```bash
   mtr google.com
   ```

   This displays ongoing information about the route and packet loss or latency at individual hops.

---

## NAT

NAT (Network Address Translation) allows a router to translate between its public IP address and the private IP addresses of devices on the local network. It tracks connections so that return traffic can be sent to the correct device.

---

## Ports

A single IP address can support multiple services because each service can use a different port.

On Linux, `/etc/services` contains mappings between service names and port numbers.

Common transport protocols include:

- TCP
- UDP

---

## Create a Port Listener

Start a listener on port `1000`:

```bash
nc -l -p 1000
```

Connect to it from another terminal:

```bash
telnet localhost 1000
```

A connection to port `1000` can be used to send and receive text messages.




