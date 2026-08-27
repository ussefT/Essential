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
