## 📄 tcp-retransmission-analysis.md
## 🚀 Overview
TCP retransmission occurs when a packet is lost, delayed, or corrupted, and the sender must resend it.
Analyzing retransmissions helps identify network issues, latency, packet loss, or congestion.

This document explains how to capture, identify, and analyze TCP retransmissions in Wireshark using clear screenshots, filters, and explanations.

## 🧠 What is TCP Retransmission?
A TCP Retransmission happens when:
The sender does not receive an ACK in time.
The packet is considered lost.
TCP resends the missing segment.
Retransmission is a recovery mechanism, not a failure itself—but frequent retransmissions indicate a problem.


##🧰 Useful Filters
To Show all TCP retransmissions:
tcp.analysis.retransmission

To Show fast retransmissions:
tcp.analysis.fast_retransmission

To Show duplicate ACKs:
tcp.analysis.duplicate_ack

To Show lost segments:
tcp.analysis.lost_segment

To Show all TCP analysis events:
tcp.analysis.flags


## 🧩 Types of TCP Retransmissions
1️⃣ Regular Retransmission

Triggered due to timeout (RTO – Retransmission Timeout).
Wireshark shows:
[TCP Retransmission]

## Useful for identifying:
High latency
Packet loss
Network instability

2️⃣ Fast Retransmission
Occurs when sender receives 3 duplicate ACKs, indicating a missing segment.
Shown as:
[TCP Fast Retransmission]
Useful for:
Detecting packet loss
Checking window congestion behavior
3️⃣ Spurious Retransmission
Occurs when the sender incorrectly thinks a packet was lost.
Shown as:
[TCP Spurious Retransmission]
Indicates:
Timing issues
Reordering
Unnecessary retransmissions


## 🔎 Packet Analysis
[TCP Retransmission] 11291 → 443 [ACK] Seq=3408 Ack=2459 Win=65024 Len=1392
📌 Analysis
Sequence Number: 3408
Next Sequence: 4800
ACK Number: 2459
Data Len: 1392 bytes
Wireshark says: This frame is a (suspected) retransmission.

🧠 What this means
The original packet with Seq=3408 was not acknowledged in time, so the sender retransmitted it.
🛑 Common Causes of TCP Retransmissions
1. Network Congestion
   - Buffers full, packets dropped.
2. Wireless Interference
   - WiFi packet loss due to noise, distance.
3. Routing Changes
   - Causes packet reordering or loss.
4. Hardware Issues
   - Faulty NICs, cables, switches.
5. Firewall / IDS Drops
   - Security devices silently dropping packets.
6. Server Overload
   - Slow ACKs and timeouts.