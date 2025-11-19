## 📄 DHCP-Process-Analysis.md
## 🚀 Overview
DHCP (Dynamic Host Configuration Protocol) automatically assigns IP addresses and network configuration to clients.
It uses a 4-step communication process known as DORA:
Discover → Offer → Request → Acknowledge
This analysis explains how to capture, identify, and understand each step of the DHCP process in Wireshark.

## 🧠 What is DHCP?
DHCP is used to dynamically provide devices with:
IP Address
Subnet Mask
Default Gateway
DNS Server
Lease Time
It operates over UDP (Ports 67/68) and uses broadcast communication for most steps.

## 🔁 DHCP DORA Process

## 1️⃣ DHCP Discover
Client → Broadcast
The client searches for a DHCP server.
Frame number
Source IP: 0.0.0.0
Destination: 255.255.255.255
Transaction ID : 0x5f13541c
Bootp flags: 0x0000 (Unicast)
DHCP Option 53 = 1 (Discover)
Parameter Request List:
     (1) Subnet Mask
     (3) Router
     (6) Domain Name Server
     (15) Domain Name
     (31) Perform Router Discover
     (33) Static Route
     (43) Vendor-Specific Information
     (44) NetBIOS over TCP/IP Name Server
     (46) NetBIOS over TCP/IP Node Type
     (47) NetBIOS over TCP/IP Scope
     (119) Domain Search
     (121) Classless Static Route
     (249) Private/Classless Static Route (Microsoft)
     (252) Private/Proxy autodiscovery

🔍 Filter:
bootp.option.type == 53 && bootp.option.value == 1


## 2️⃣ DHCP Offer
Server → Client
The server offers an available IP address.
Source: 20:57:af:8f:e7:00 (Servers MAC address)
Destination: 4c:49:6c:84:d6:b3
Source Address: 192.168.1.1
Destination Address: 255.255.255.255
Transaction ID: 0x5f13541c
(client) IP address: 192.168.1.6 (Offered IP address)
Option: (53) DHCP Message Type (Offer)
IP Address Lease Time: 1 day (86400)

🔍 Filter:
bootp.option.type == 53 && bootp.option.value == 2


## 3️⃣ DHCP Request
Client → Server
Client requests the offered IP.
Message type: Boot Request (1)
Transaction ID: 0x5f13541c
Option: (50) Requested IP Address (192.168.1.6)
Option: (54) DHCP Server Identifier (192.168.1.1)
Option: (53) DHCP Message Type (Request)

🔍 Filter:
bootp.option.type == 53 && bootp.option.value == 3


## 4️⃣ DHCP ACK
Server → Client
The server approves and assigns the IP.
Message type: Boot Reply (2)
Transaction ID: 0x5f13541c
(client) IP address: 192.168.1.6 (officially assigned IP)
Option: (53) DHCP Message Type (ACK)
IP Address Lease Time: 1 day (86400)

🔍 Filter:
bootp.option.type == 53 && bootp.option.value == 5

## 🧰 Useful Filters
dhcp
bootp
bootp.option.type == 53
bootp.ip.yiaddr
bootp.id == <transaction_id>