# Network

- [Linux]()
- [Base Network]()
> - [ping]()
> - [curl]()
> - [wget]()
- [Protocol]()
- [Port]()
- [Dns]()


## Base Network
🔺 ip 
> A unique identifier for a device on a network. 
> IPv4: 192.168.1.10
> IPv6: fe80::1

🔺 Subnet Mask
> Determines which part of the IP address represents the network and which represents the host.
> Example: 255.255.255.0 or /24 (/24 means 24 bit for host and another bit 0 for client)

🔺 Gateway
> The exit route for a system to access the internet.
> Example: 192.168.1.1

🔺MAC Address
> Hardware identifier of the network card.


🔺Interface
> Each network card has an interface:
> eth0, wlan0, enp0s3, etc.

Show IP addresses of all interfaces.
```bash
ip route
```
Show routes and gateway
```bash
ip link
```
Check internet Connectivity
- [ping]()
```bash
ping 8.8.8.8
```
Test HTTP connection:
- [curl]()
- [wget]()
```bash
curl google.com
wget google.com
```

#### Maange Network Services
Ubuntu:
```bash
sudo systemctl restart systemcd-network
sudo systemctl status systemcd-network
```
RedHat:
```bash
sudo systemctl restart NetworkManager
sudo systemctl status NetworkManager
```
#### Assign static IP
Add static IP
```bash
sudo ip addr add 192.168.11.30/24 dev enp0s3
```
Remove static IP
```bash
sudo ip addr del 192.168.11.30/24 dev enp0s3
```

#### DHCP and Automatic IP
```bash
sudo dhclient -r
sudo dhclient
```

## Protocol

A protocol is a set of rules that define how data is transmitted across a network.

- TCP – Reliable, connection-oriented

- UDP – Fast, connectionless

- [HTTP / HTTPS]() – Web communication

- FTP / SFTP – File transfer

- SMTP / POP3 / IMAP – Email communication

- [DNS]() – Resolves domain names to IP addresses

- SSH – Secure remote access

## Port
A port is a numeric identifier that the operating system uses to route network traffic to the correct application.
When a device receives data, ports define which service or program should handle it

<div dir="rtl">
پورت (Port) یک عدد است که به سیستم‌عامل کمک می‌کند برای هر برنامه یا سرویس شبکه، یک مسیر ارتباطی مشخص تعریف کند.
وقتی کامپیوتر شما دیتایی را دریافت می‌کند، این داده باید به برنامه‌ی درست ارسال شود. پورت‌ها این تفکیک را انجام می‌دهند.
</div>

| Port     | Service    |
| -------- |------------|
| **80**   | [HTTP]()   |
| **443**  | [HTTPS]()  |
| **22**   | SSH        |
| **21**   | FTP        |
| **25**   | SMTP       |
| **53**   | DNS        |
| **110**  | POP3       |
| **3306** | MySQL      |
| **5432** | PostgreSQL |

## Dns
✅ What is DNS?

DNS (Domain Name System) is the Internet’s phonebook.
It translates human-readable names → machine-readable IP addresses.

### Dns client debain/ubuntu base
#### Client:
```bash
sudo resolvectl dns eth0 1.1.1.1 8.8.8.8 # on interface eht0 set dns
```
or edit file:
```bash
vi /etc/systemd/resolved.conf
# add 
#DNS=1.1.1.1 8.8.8.8
```

##### Server:
```bash

sudo apt update
sudo apt install bind9 bind9utils bind9-doc -y
```


### Dns client redhat base
#### Client:
Edit this file:
```bash
vi /etc/resolv.conf
# nameserver 1.1.1.1
# nameserver 8.8.8.8
```
#### Server:



## ping
ping is a network diagnostic tool used to check if your computer can reach another device on a network (LAN or the Internet). It also measures how long it takes for a message to go there and back (round-trip time).

A ping request typically uses the ICMP (Internet Control Message Protocol) and does not operate through a specific port. Instead, it sends Echo Request messages to the target host to check its reachability and measures the round-trip time.
```bash 
ping google.com
```
| Option          | Example                   | Purpose                                               |
| --------------- | ------------------------- | ----------------------------------------------------- |
| `-c <count>`    | `ping -c 5 google.com`    | Send only 5 packets then stop                         |
| `-i <interval>` | `ping -i 2 google.com`    | Send a ping every 2 seconds (default 1 sec)           |
| `-s <size>`     | `ping -s 1000 google.com` | Send larger packets (default 56 bytes)                |
| `-t <ttl>`      | `ping -t 64 google.com`   | Set TTL (time-to-live) for packet                     |
| `-W <timeout>`  | `ping -W 2 google.com`    | Wait 2 seconds for a reply                            |
| `-q`            | `ping -c 5 -q google.com` | Quiet output, only summary                            |
| `-a`            | `ping -a google.com`      | Audible ping (beeps when response received)           |
| `-f`            | `ping -f google.com`      | Flood ping (high-speed, very advanced, requires sudo) |


## curl
curl (Client URL) is a command-line tool to transfer data to or from a server using many protocols like HTTP, HTTPS, FTP, etc.
