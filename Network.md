# Network

- [Linux]()
- [Protocol]()
- [Port]()
- [Dns]()
- []()


## Protocol






## Port




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

