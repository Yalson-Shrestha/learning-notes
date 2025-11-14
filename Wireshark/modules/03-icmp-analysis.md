# ICMP Analysis Using Wireshark

## 🎯 Objective
To analyze ICMP (Internet Control Message Protocol) packets using Wireshark and understand how ping, echo requests, echo replies, and error messages work at the packet level.


## 🧠 What is ICMP?

ICMP is a Layer 3 protocol used for network diagnostics and communication error reporting.  
It is most commonly seen with:

- **Echo Request** (ping)
- **Echo Reply**
- **Destination Unreachable**
- **Time Exceeded (TTL exceeded)**
- **Redirect Messages**

ICMP is not used for data transfer — only for control and error messages.


## ⚙️ Capture Setup

To generate ICMP traffic for analysis:

1. Start capturing on the main network interface.
2. Run the command:
   ```bash
   ping 8.8.8.8 -c 4


## 🔍 ICMP Packet Analysis

### 📨 ICMP Echo Request
Key fields:
- **Type:** 8 (Echo Request)
- **Code:** 0  
- **Source IP:** 192.168.1.5
- **Destination IP:** 8.8.8.8

Meaning: The host is asking if the destination is reachable.

---

### 📨 ICMP Echo Reply
Key fields:
- **Type:** 0 (Echo Reply)
- **Code:** 0
- **Source IP:** 8.8.8.8
- **Destination IP:** 192.168.1.5

Meaning: The target host responded, confirming network reachability.


## 🧪 Useful ICMP Filters in Wireshark

| Purpose | Filter |
|--------|--------|
| Show only ICMP | `icmp` |
| Echo Requests only | `icmp.type == 8` |
| Echo Replies only | `icmp.type == 0` |
| Destination Unreachable | `icmp.type == 3` |
| Time Exceeded | `icmp.type == 11` |
| Match specific sequence number | `icmp.seq == 1` |