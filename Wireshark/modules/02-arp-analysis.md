# ARP (Address Resolution Protocol) Analysis using Wireshark

## 🎯 Objective
To analyze how ARP works at the packet level using Wireshark — understanding how devices map IP addresses to MAC addresses within a local network.

## 🧠 What is ARP?

ARP (Address Resolution Protocol) is used to map an IP address (Layer 3) to a MAC address (Layer 2).  
It operates within a local network segment and helps devices discover the hardware address of another device.

- **ARP Request:** "Who has 192.168.1.5? Tell 192.168.1.10"
- **ARP Reply:** "192.168.1.5 is at 00:1A:2B:3C:4D:5E"

ARP messages are broadcast within the local subnet and are crucial for communication in Ethernet-based networks.


## ⚙️ Capture Setup

1. Open Wireshark and select your active network interface (e.g., `eth0` or `wlan0`).
2. Start a capture.
3. In a terminal, run:
   ```bash
   ping 172.19.147.123 (my gateway address)
   (This triggers an ARP request if the IP is not in the cache.)
4. Stop the capture after a few seconds.
5. Apply the display filter: arp

## 🔍 Packet Analysis

### 🧾 ARP Request
- **Source MAC:** 4c:49:6c:84:d6:b3 
- **Destination MAC:** ff:ff:ff:ff:ff:ff (broadcast)  
- **Opcode:** 1 (request)
- **Sender IP:** 192.168.1.5 
- **Target IP:** 192.168.1.2

Meaning: The host 192.168.1.5 is asking, “Who has 192.168.1.2?”

---

### 📨 ARP Reply
- **Source MAC:** 54:d6:0d:48:7e:13  
- **Destination MAC:** 4c:49:6c:84:d6:b3  
- **Opcode:** 2 (reply)
- **Sender IP:** 192.168.1.2 
- **Target IP:** 192.168.1.5  

Meaning: The device at 192.168.1.2 replies with its MAC address 54:d6:0d:48:7e:13.

## 🧩 Interpretation

- The ARP Request was **broadcast**, while the ARP Reply was **unicast** to the requester.  
- This exchange allows the sender to update its ARP cache with the MAC address of the destination.  
- Without ARP, local devices couldn’t communicate using IP since MAC addresses are needed for Layer 2 delivery.
