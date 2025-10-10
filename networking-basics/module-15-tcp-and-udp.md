# 📘 Module 15: TCP and UDP

# 📘 Module 15.1: TCP and UDP Operation

## 📌 Key Concepts
- **TCP (Transmission Control Protocol)**: Reliable, connection-oriented with acknowledgments and sequencing
- **UDP (User Datagram Protocol)**: Unreliable, connectionless with minimal overhead
- **Port Numbers**: Identify applications/services in transport layer communications
- **Sequencing**: TCP uses sequence numbers for ordering and reliability
- **Acknowledgments**: TCP confirms packet delivery; UDP has no acknowledgments
- **Use Cases**: TCP for critical data, UDP for real-time/streaming applications

---

## 🔧 Technical Details

### UDP (User Datagram Protocol)
**Characteristics:**
- **Connectionless**: No established connection before data transfer
- **Minimal Overhead**: Small header size, no reliability mechanisms
- **No Guarantees**: No delivery confirmation, no ordering, no retransmission
- **Fast**: Low latency, ideal for real-time applications

**Header Structure:**
- Source Port (16 bits)
- Destination Port (16 bits)
- Length (16 bits)
- Checksum (16 bits)

**Operation:**
- Data divided into segments at transport layer
- Each segment labeled with source/destination ports
- Segments sent independently without tracking
- No retransmission of lost packets

### TCP (Transmission Control Protocol)
**Characteristics:**
- **Connection-Oriented**: Three-way handshake establishes connection
- **Reliable Delivery**: Acknowledgments confirm packet receipt
- **Sequencing**: Packets numbered for proper ordering
- **Flow Control**: Manages data transmission rate
- **Error Recovery**: Retransmits lost or corrupted packets

**Header Structure:**
- Source Port, Destination Port
- Sequence Number (32 bits)
- Acknowledgment Number (32 bits)
- Window Size, Checksum, Flags
- Options (variable)

**Operation:**
1. **Segmentation**: Data divided into numbered segments
2. **Transmission**: Segments sent with sequence numbers
3. **Acknowledgment**: Receiver confirms with ACK numbers
4. **Retransmission**: Missing segments resent based on timeouts/ACKs
5. **Reassembly**: Segments reordered using sequence numbers

### Key Differences
| Feature | TCP | UDP |
|---|---|---|
| **Reliability** | ✅ Acknowledgment system | ❌ No delivery confirmation |
| **Ordering** | ✅ Sequence numbers | ❌ No guaranteed order |
| **Connection** | ✅ Connection-oriented | ❌ Connectionless |
| **Speed** | Slower (overhead) | Faster (minimal overhead) |
| **Overhead** | Higher (20+ byte header) | Lower (8 byte header) |
| **Retransmission** | ✅ Automatic | ❌ None |
| **Flow Control** | ✅ Window sizing | ❌ None |

### Port Number Usage
**Common Port Examples:**
- **TCP Port 80**: HTTP web traffic
- **TCP Port 443**: HTTPS secure web
- **UDP Port 53**: DNS queries
- **UDP Port 123**: NTP time synchronization
- **TCP/UDP Port 25**: SMTP email

---

## 🌐 Real-World Examples

**UDP Use Cases:**
**Voice over IP (VoIP):**
- Real-time voice communication
- Occasional dropped packets unnoticeable
- Retransmission would cause more disruption than packet loss

**Video Streaming:**
- Live broadcasts, online gaming
- Minor packet loss acceptable
- Buffering handles minor inconsistencies

**DNS Queries:**
- Fast name resolution
- Simple request/response pattern
- If response lost, client retries

**TCP Use Cases:**
**Web Browsing (HTTP/HTTPS):**
- Critical that all webpage data arrives
- Text, images must be complete and in order
- Port 80 (HTTP), 443 (HTTPS)

**File Transfers (FTP):**
- Entire files must transfer completely
- Corruption or missing data makes files unusable
- Port 21 (control), 20 (data)

**Email (SMTP):**
- Messages must be delivered completely
- Financial information, important communications
- Port 25

**Banking Transactions:**
- Financial data integrity critical
- Missing packets could mean lost money
- Sequence numbers ensure complete transactions

**Adaptive Behavior Examples:**
**TCP in Good Conditions:**
- Large window sizes (1000s of packets)
- Infrequent acknowledgments
- High throughput

**TCP in Poor Conditions:**
- Small window sizes (few packets)
- Frequent acknowledgments
- Lower throughput but reliable

---

## 🎯 My Takeaways
- **TCP and UDP serve different needs** - no "better" protocol, just different use cases
- **Reliability comes at a cost** - TCP's overhead is necessary for critical data
- **UDP's simplicity enables real-time performance** - perfect for applications where speed matters more than perfection
- **Port numbers create application-level addressing** - allowing multiple services on single device
- **TCP's adaptive window sizing** intelligently responds to network conditions
- **Sequence numbers solve the ordering problem** for data that travels multiple paths
- **The choice depends on application requirements** - financial data needs TCP, live video prefers UDP
- **Understanding these protocols helps troubleshoot** network performance issues

---


# 📘 Module 15.2: Port Numbers

## 📌 Key Concepts
- **Port Numbers**: Identify specific applications and services in network communications
- **Well-Known Ports**: 1-1023 (standard services like HTTP, FTP, DNS)
- **Registered Ports**: 1024-49151 (organization-registered applications)
- **Private Ports**: 49152-65535 (dynamic client ports)
- **Sockets**: Combination of IP address + port number
- **netstat Command**: Utility to view active network connections
- **Client-Server Communication**: Clients use dynamic ports, servers use well-known ports

---

## 🔧 Technical Details

### Port Number Categories
**Well-Known Ports (1-1023):**
- Standard services assigned by IANA
- Servers listen on these ports
- Examples: HTTP (80), FTP (21), SSH (22), SMTP (25)

**Registered Ports (1024-49151):**
- Can be used as source or destination ports
- Organizations register specific applications
- Examples: Microsoft SQL Server (1433), Oracle (1521)

**Private Ports (49152-65535):**
- Also called dynamic or ephemeral ports
- Used as source ports by clients
- Randomly assigned by client operating systems

### Common Well-Known Ports
| Port | Protocol | Service | Description |
|---|---|---|---|
| **20/21** | TCP | FTP | File Transfer (Data/Control) |
| **22** | TCP | SSH | Secure Shell |
| **23** | TCP | Telnet | Remote terminal |
| **25** | TCP | SMTP | Email sending |
| **53** | TCP/UDP | DNS | Domain Name System |
| **67/68** | UDP | DHCP | Dynamic Host Configuration |
| **69** | UDP | TFTP | Trivial File Transfer |
| **80** | TCP | HTTP | Web browsing |
| **110** | TCP | POP3 | Email retrieval |
| **143** | TCP | IMAP | Email management |
| **443** | TCP | HTTPS | Secure web browsing |

### Socket Pairs
**Socket Definition:** IP Address + Port Number

**Client Socket Example:**
- `192.168.1.5:1099` (Client IP + Dynamic Port)

**Server Socket Example:**
- `192.168.1.7:80` (Server IP + HTTP Port)

**Socket Pair:**
- `192.168.1.5:1099, 192.168.1.7:80`
- Uniquely identifies a specific connection

### Client-Server Communication Process
**Web Request Example:**
1. **Client** picks random source port (5305)
2. **Request**: Source port 5305 → Destination port 80
3. **Server** responds: Source port 80 → Destination port 5305
4. **Client** routes response to correct application using port 5305

**Multiple Simultaneous Connections:**
- Web browser: Source port 5305 → Destination port 80
- FTP client: Source port 5307 → Destination port 21
- Each application gets unique source port

### netstat Command Utility
**Purpose:** Display active network connections and ports

**Basic Usage:**
bash
netstat

**Numerical Output:**
netstat -n  # Shows IPs and ports numerically

**Sample Output:**
Proto  Local Address          Foreign Address        State
TCP    192.168.1.124:3126     192.168.0.2:139        ESTABLISHED
TCP    192.168.1.124:3158     207.138.126.152:80     ESTABLISHED
TCP    192.168.1.124:3166     www.cisco.com:80       ESTABLISHED


**Key Information:**

Protocol: TCP or UDP

Local Address: Your IP and port

Foreign Address: Remote IP and port

State: Connection status (ESTABLISHED, LISTENING, etc.)


## 🌐 Real-World Examples

**Web Browsing Session:**
Client: 192.168.1.105 (random port 5305)
Server: 93.184.216.34 (port 80)

Request:  192.168.1.105:5305 → 93.184.216.34:80
Response: 93.184.216.34:80 → 192.168.1.105:5305

**Multiple Services on One Server:**
Web Server: 203.0.113.10
- HTTP: Listening on port 80
- FTP: Listening on port 21
- SSH: Listening on port 22
- Email: Listening on port 25

Different clients connect to different ports for different services


**Simultaneous Applications:**

User Activities:
- Web browsing: Port 5305 → 80
- Email client: Port 5306 → 110 (POP3)
- File transfer: Port 5307 → 21 (FTP)
- DNS query: Port 5308 → 53 (DNS)

All running concurrently on same device


**Security Monitoring with netstat:**
Suspicious Connection Found:
TCP    192.168.1.105:4444    198.51.100.23:1234    ESTABLISHED

Investigation:
- Port 4444: Common backdoor port
- Unknown foreign IP
- Indicates potential security breach


**🎯 My Takeaways**
-**Port numbers enable application multiplexing** - multiple services can run on single server

-**Well-known ports create standardization** - clients automatically know where to find services

-Dynamic ports allow multiple simultaneous connections from single client

-**Socket pairs uniquely identify conversations** - essential for routing responses correctly

-**Netstat is crucial for network troubleshooting and security** - reveals all active connections

-**The client-server port relationship is asymmetric** - servers use fixed ports, clients use random ports

-**Understanding ports helps with firewall configuration** - controlling which services are accessible

-**Port numbers work with both TCP and UDP** - same numbering system, different protocols