[En](https://github.com/ussefT/Essential/blob/main/Base_Network_en.md)

# Linux Networking Notes

## Set IP for Interface in Linux

```bash
ip addr show
```

مشاهده‌ی تمام interfaceهای موجود در سیستم‌عامل:

```bash
ip addr show
```

برای اضافه کردن IP به یک interface:

```bash
ip addr add 192.168.56.11/24 dev enp0s8
```

### `/24` یعنی چه؟

`/24` یعنی **24 بیت اول برای Network** و **8 بیت برای Host** استفاده می‌شود.

مثال:

```text
192.168.56.11/24

Netmask: 255.255.255.0
Network: 192.168.56.0
Host:    11
```

> به طور خلاصه: `Netmask = 255.255.255.0` مشخص می‌کند کدام قسمت IP مربوط به Network و کدام قسمت مربوط به Host است.

---

## What is Ping?

`ping` یک ابزار شبکه برای بررسی دسترسی یک سیستم به یک IP یا Host دیگر است.

برای مثال:

```bash
ping 192.168.1.10
```

در شبکه‌ی IPv4، `ping` معمولاً از **ICMP Echo Request** استفاده می‌کند و سیستم مقصد در صورت دسترسی، **ICMP Echo Reply** ارسال می‌کند.

---

## 3 Devices Connected to a Switch

فرض کنید 3 دستگاه به یک Switch متصل هستند.

وقتی:

> Device A → ping → Device B

و Ping موفق باشد، Switch چگونه کار می‌کند؟

### How does a Switch work with IP if it works with MAC addresses?

Switch در لایه‌ی Data Link یعنی **Layer 2** کار می‌کند و برای Forward کردن Frameها از **MAC Address** استفاده می‌کند.

در Switch یک جدول به نام **CAM Table (Content Addressable Memory)** وجود دارد.

برای مثال:

```text
MAC Address          Port
AA:AA:AA:AA:AA:01    Port 1
BB:BB:BB:BB:BB:02    Port 2
CC:CC:CC:CC:CC:03    Port 3
```

وقتی یک Frame برای اولین بار وارد Switch می‌شود، Switch می‌تواند از **Source MAC Address** و پورتی که Frame از آن وارد شده است یاد بگیرد و آن را در CAM Table ذخیره کند.

اگر MAC مقصد ناشناخته باشد، Switch Frame را به پورت‌های دیگر **Flood** می‌کند تا مقصد پیدا شود.

بعد از یادگیری MAC Address، Switch می‌تواند Frame را فقط به پورت مربوط به مقصد ارسال کند.

---

## How Does the OS Know Which MAC Belongs to an IP?

سیستم‌عامل برای پیدا کردن MAC Address مربوط به یک IPv4 از **ARP (Address Resolution Protocol)** استفاده می‌کند.

### ARP

ARP برای پیدا کردن:

```text
IP Address → MAC Address
```

است.

مثال:

```text
Who has 192.168.1.20?
Tell 192.168.1.10
```

دستگاهی که IP `192.168.1.20` را دارد، MAC Address خود را در پاسخ اعلام می‌کند.

برای مشاهده‌ی اطلاعات ARP در Linux می‌توان از این دستورها استفاده کرد:

```bash
ip neigh
```

در سیستم‌هایی که ابزار قدیمی `arp` نصب باشد:

```bash
arp -n
```

برای حذف یک entry:

```bash
sudo arp -d 192.168.1.20
```

یا روش جدیدتر:

```bash
sudo ip neigh del 192.168.1.20 dev eth0
```

وقتی Ping برای اولین بار انجام می‌شود، ممکن است ابتدا ARP انجام شود و نتیجه در Neighbor/ARP cache ذخیره شود.

---

## Switch Can Have a Loop

بله، اگر بین Switchها مسیرهای اضافی ایجاد شود، ممکن است **Layer 2 Loop** ایجاد شود.

Loop می‌تواند باعث مشکلاتی مانند:

- Broadcast Storm
- Duplicate Frames
- MAC Table Instability

شود.

برای جلوگیری از این مشکل، پروتکل‌هایی مانند **STP (Spanning Tree Protocol)** استفاده می‌شوند.

---

# OSI Layers

مدل OSI دارای 7 لایه است:

| Layer | Name |
|---:|---|
| 7 | Application |
| 6 | Presentation |
| 5 | Session |
| 4 | Transport |
| 3 | Network |
| 2 | Data Link |
| 1 | Physical |

مثال ابزارها و پروتکل‌ها:

```text
Layer 7 → HTTP, DNS, SSH
Layer 4 → TCP, UDP
Layer 3 → IP, ICMP
Layer 2 → Ethernet, MAC, ARP
Layer 1 → Cable, Fiber, Radio
```

---

# DHCP

**DHCP (Dynamic Host Configuration Protocol)** می‌تواند IP Address را به صورت خودکار به دستگاه‌ها بدهد.

DHCP در حالت معمول از این پورت‌ها استفاده می‌کند:

```text
Server → UDP 67
Client → UDP 68
```

این یعنی:

```text
Client source port: 68
Server destination port: 67
```

### DHCP Discover

در شروع کار، Client هنوز IP ندارد، بنابراین می‌تواند از:

```text
Source IP:      0.0.0.0
Destination IP: 255.255.255.255
```

استفاده کند.

فرآیند معمول DHCP:

```text
DHCP Discover
       ↓
DHCP Offer
       ↓
DHCP Request
       ↓
DHCP ACK
```

### DHCP ACK چیست؟

**DHCP ACK (Acknowledgement)** پیام تأیید DHCP Server است.

در این مرحله Server به Client اعلام می‌کند که تنظیمات پیشنهادی را تأیید کرده است؛ برای مثال:

```text
IP Address
Netmask
Default Gateway
DNS Server
Lease Time
```

پس به صورت ساده:

```text
Offer  → Server پیشنهاد IP می‌دهد
Request → Client درخواست همان IP را می‌کند
ACK    → Server درخواست را تأیید می‌کند
```

---

## Install / Search DHCP Server Package

برای جست‌وجوی package:

```bash
apt search isc-dhcp-server
```

> در متن اصلی `dehcp-server` نوشته شده بود؛ نام رایج package در Debian/Ubuntu برای DHCP Server برابر `isc-dhcp-server` است.

### DHCP Configuration

در Debian/Ubuntu، فایل تنظیمات اصلی ISC DHCP Server معمولاً:

```text
/etc/dhcp/dhcpd.conf
```

است.

برای مثال می‌توان گزینه‌هایی مانند Domain Name را تنظیم کرد:

```conf
option domain-name "HI";
```

همچنین می‌توان یک subnet تعریف کرد:

```conf
subnet 192.168.1.0 netmask 255.255.255.0 {
}
```

بعد از تغییر تنظیمات:

```bash
sudo systemctl restart isc-dhcp-server
```

### Example

دستگاه‌ها به Switch متصل هستند و یکی از دستگاه‌ها `isc-dhcp-server` را اجرا می‌کند. در این حالت DHCP Server می‌تواند به دستگاه‌های دیگر IP و سایر تنظیمات شبکه را به صورت خودکار ارائه دهد.

---

## DHCP Client

برای آزاد کردن IP فعلی:

```bash
sudo dhclient -r eth0
```

برای گرفتن IP به صورت خودکار:

```bash
sudo dhclient eth0
```

---

## Important: DHCP Uses Broadcast

در ابتدای فرآیند DHCP، Client هنوز IP مشخصی ندارد و برای پیدا کردن DHCP Server از Broadcast استفاده می‌کند.

به همین دلیل پیام اولیه می‌تواند برای تمام دستگاه‌های Broadcast Domain ارسال شود.

> اگر تنظیمات شبکه یا IP Configuration اشتباه باشد، DHCP ممکن است درست کار نکند.

---

# What is Netmask & Host?

برای مثال:

```text
IP:      192.168.1.0/24
Netmask: 255.255.255.0
```

در `/24`:

```text
Network: 192.168.1
Host:    0 - 255
```

اما در یک subnet معمولی `192.168.1.0/24`:

```text
Network Address:   192.168.1.0
Usable Hosts:      192.168.1.1 - 192.168.1.254
Broadcast Address: 192.168.1.255
```

---

# IP Range

در روش کلاسیک IPv4، IANA بازه‌ها را به کلاس‌های A, B و C تقسیم می‌کرد:

```text
Class A: 0.0.0.0     - 127.255.255.255
Class B: 128.0.0.0   - 191.255.255.255
Class C: 192.0.0.0   - 223.255.255.255
```

امروزه برای مسیریابی، **CIDR** و Prefix Length مثل `/8`، `/16` و `/24` بسیار مهم‌تر از Classful Networking هستند.

---

# Routing

وقتی سیستم می‌خواهد یک IP را ارسال کند، Routing Table مشخص می‌کند Packet باید از کدام مسیر و interface ارسال شود.

برای اضافه کردن یک route مشخص:

```bash
ip route add [specificIP]/24 dev enp0s4
```

منظور از `[specificIP]` یک **Network Address** است.

مثال:

```bash
sudo ip route add 192.168.20.0/24 dev enp0s4
```

این route می‌گوید برای شبکه‌ی `192.168.20.0/24` از interface `enp0s4` استفاده شود.

> صرفاً فرستادن Packet به یک Switch به این معنی نیست که مقصد حتماً پاسخ خواهد داد؛ مقصد باید وجود داشته باشد و مسیر برگشت هم مناسب باشد.

برای یک شبکه دیگر:

```bash
ip route add [senderIP]/24 dev eth0
```

مثال:

```bash
sudo ip route add 10.10.10.0/24 dev eth0
```

اگر IP مقصد در Routing Table شناخته‌شده نباشد، می‌توان از Default Route استفاده کرد:

```bash
ip route add default dev eth0
```

اما در شبکه‌های معمول، Default Route بیشتر به Gateway اشاره می‌کند:

```bash
sudo ip route add default via 192.168.1.1 dev eth0
```

---

# Router — Layer 3

Router در اصل در **Layer 3 (Network Layer)** کار می‌کند و با IP Address و Routing Table کار می‌کند.

### When a Device Connects to a Router

Router برای خودش interface دارد و هر interface می‌تواند IP داشته باشد.

برای مشاهده‌ی interfaceها:

```bash
ip addr show
```

Example:

```text
Router
 ├── eth0 → 192.168.1.1/24
 └── eth1 → 10.0.0.1/24
```

هر interface روتر معمولاً یک IP متناسب با شبکه‌ای که به آن متصل است دارد.

---

# Give All Devices a Route

برای مشاهده‌ی Routing Table:

```bash
ip route
```

ممکن است خروجی چیزی شبیه این باشد:

```text
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.50
```

---

## Example: `ping 8.8.8.8`

وقتی اجرا می‌کنیم:

```bash
ping 8.8.8.8
```

به صورت ساده:

1. OS بررسی می‌کند مقصد در همان Network قرار دارد یا نه.
2. Routing Table را بررسی می‌کند.
3. اگر مقصد Route مستقیم نداشته باشد، Default Route را بررسی می‌کند.
4. Packet به Gateway/Router ارسال می‌شود.
5. Router Packet را بر اساس Routing Table به سمت مقصد Forward می‌کند.

---

# Router Information

وقتی وارد پنل Router می‌شویم، ممکن است چیزی شبیه این ببینیم:

```text
IP Address:  192.168.1.50
Netmask:     255.255.255.0
Gateway:     192.168.1.1
```

معنی:

```text
IP Address
→ IP اختصاص داده شده به Interface دستگاه.

Netmask
→ مشخص می‌کند Network و Host کدام بخش IP هستند.

Gateway
→ دستگاهی که Packetهای خارج از Network محلی معمولاً به سمت آن ارسال می‌شوند.
```

---

# TTL

**TTL (Time To Live)** یک مقدار در Header مربوط به IP است که برای محدود کردن تعداد Router Hopها استفاده می‌شود.

به صورت ساده:

```text
Packet
  ↓
Router 1 → TTL - 1
  ↓
Router 2 → TTL - 1
  ↓
Router 3 → TTL - 1
```

اگر TTL به `0` برسد، Router معمولاً Packet را Drop می‌کند و پیام ICMP مربوط به **Time Exceeded** را ارسال می‌کند.

---

## Traceroute

برای مشاهده‌ی مسیر عبور Packet:

```bash
traceroute 4.2.2.4
```

در صورت نبودن دستور:

```bash
sudo apt install traceroute
```

`traceroute` از تغییرات TTL و پیام‌های ICMP برای آشکار کردن Hopهای مسیر استفاده می‌کند.

---

# Networking Questions

## فرض کنید کارت شبکه دو کامپیوتر را به یک سوییچ وصل کرده و برای هر کدام از کارت شبکه‌ها IPهای `150.70.10.10/8` و `150.90.4.1/8` را تنظیم می‌کنیم، آیا این کامپیوترها Ping همدیگر را دارند و چرا؟

### Answer

بله، هر دو کامپیوتر Ping همدیگر را دارند.

چون:

```text
150.70.10.10/8
150.90.4.1/8
```

با `/8` دارای Netmask زیر هستند:

```text
255.0.0.0
```

بنابراین Network هر دو:

```text
150.0.0.0/8
```

است.

پس هر دو کامپیوتر در **یک شبکه قرار دارند** و چون مستقیماً به یک **Switch** متصل هستند، برای برقراری ارتباط با یکدیگر به Router نیاز ندارند.

روند ساده:

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

قبل از ارسال ترافیک IP، PC A می‌تواند با استفاده از ARP، MAC Address مربوط به `150.90.4.1` را پیدا کند و Frame را به MAC مقصد بفرستد.

**نتیجه: بله، Ping دارند.**

---

## هر کدام از کارت شبکه‌های روتر و سوییچ به ترتیب از راست به چپ آیا باید یک IP بگیرند یا نه؟

### Answer

**Router: بله، معمولاً هر Interface روتر که در لایه 3 برای یک شبکه استفاده می‌شود، IP Address دارد.**

مثال:

```text
Router
eth0 → 192.168.1.1/24
eth1 → 10.0.0.1/24
```

**Switch معمولی Layer 2: خیر، Portهای Switch برای Forwarding به IP نیاز ندارند و با MAC Address کار می‌کنند.**

اما خود Switch ممکن است برای **Management** یک IP روی یک SVI/Management Interface داشته باشد.

مثال:

```text
Switch
Port 1 → PC
Port 2 → PC
Port 3 → Router

Management IP → 192.168.1.2/24
```

پس:

```text
Router Interface → IP دارد
Switch Port      → معمولاً IP ندارد
Switch Management Interface → می‌تواند IP داشته باشد
```

---

## مقدار IP ورژن 4 چند بیت است؟

**32-bit**

مثال:

```text
192.168.1.10
```

در IPv4 چهار Octet داریم و هر Octet برابر 8 بیت است:

```text
8 + 8 + 8 + 8 = 32 bits
```

---

## مقدار IP ورژن 6 چند بیت است؟

**128-bit**

مثال:

```text
2001:db8::1
```

IPv6 دارای 128 بیت است.
