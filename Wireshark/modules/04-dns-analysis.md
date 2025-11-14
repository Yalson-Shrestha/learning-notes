# DNS Analysis Using Wireshark

## 🎯 Objective
To analyze DNS (Domain Name System) packets using Wireshark and understand how domain name resolution works at the packet level, including queries, responses, and record types.

## 🧠 What is DNS?

DNS is a Layer 7 protocol that translates human-readable domain names into IP addresses. Key components:

- **DNS Query** - Request for domain information
- **DNS Response** - Reply containing the requested records
- **Record Types**: A, AAAA, CNAME, MX, NS, PTR
- **Port 53** - Used for both UDP (queries) and TCP (zone transfers)

## ⚙️ Capture Setup

To generate DNS traffic for analysis:

1. Start capturing on the main network interface
2. Visit any website on browser.

## 🔍 DNS Packet Analysis
📨 DNS Query Packet
Key fields in Wireshark:

- **Transaction ID** - 0x0eac

- **Flags:** 0x0200 Standard query

- **Questions:** 1

- **Query Name:** www.instagram.com

- **Query Type:** A (IPv4)

- **Meaning**: Client asking DNS server to resolve a domain name.


## 📨 DNS Response Packet
Key fields:

- **Flags:** 0x8180 Standard query response, no error

- **Answers:** 2

- **Authority:** 0

- **Additional:** 0

- **Answer Section:** 57.114.176.34

- **Meaning:** DNS server providing the resolved IP address.


## Types of DNS Records Observed

A (IPv4),
AAAA (IPv6),
CNAME (Alias),
MX (Mail servers),
NS (Name servers),
PTR (Reverse lookup),


## 🧪 Useful DNS Filters in Wireshark
|Purpose          |	Filter |
|-----------------|---------|
|Show only DNS	     |dns  |
|DNS Queries only	|dns.flags.response == 0  |
|DNS Responses only	|dns.flags.response == 1  |
|Specific domain	|dns.qry.name contains "google"  |
|A record queries	|dns.qry.type == 1  |
|Failed responses	|dns.flags.rcode != 0  |
|DNS over TCP	     |tcp.port == 53  |