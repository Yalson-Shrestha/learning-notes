# 📘 Module 7: The Access Layer

# 📘 Module 7.1: Encapsulation and Ethernet Frame

## 📌 Key Concepts
- **Ethernet Frame Structure**: Specific format for local network communication between NICs
- **MAC Addresses**: Unique hardware addresses for source and destination devices
- **Encapsulation Process**: Wrapping data with headers/trailers for delivery
- **De-encapsulation**: Reverse process of removing headers to access original data
- **Frame Fields**: Preamble, SFD, MAC addresses, length/type, data, and FCS
- **Error Detection**: Frame Check Sequence ensures data integrity during transmission

---

## 🔧 Technical Details

### Ethernet Frame Structure
| Field | Size (Bytes) | Purpose |
|---|---|---|
| **Preamble** | 7 | Synchronizes receiving NIC with incoming bits |
| **Start Frame Delimiter (SFD)** | 1 | Marks beginning of actual frame data |
| **Destination MAC Address** | 6 | Hardware address of receiving device |
| **Source MAC Address** | 6 | Hardware address of sending device |
| **Length/Type** | 2 | Either data length or protocol type (IPv4/IPv6) |
| **Data/Payload** | 46-1500 | Encapsulated network layer packet |
| **Frame Check Sequence (FCS)** | 4 | Error detection using CRC checksum |

### Encapsulation Process
**Analogy**: Letter in Envelope
- **Data** = Letter content
- **Frame Headers** = Envelope with addresses
- **Encapsulation** = Putting letter in envelope
- **De-encapsulation** = Removing letter from envelope

**Network Encapsulation**:
1. Application data wrapped in Transport layer header (TCP/UDP)
2. Transport segment wrapped in Network layer header (IP)
3. IP packet wrapped in Data Link header/footer (Ethernet frame)
4. Frame converted to bits for Physical transmission

### Key Functions
**MAC Addresses**:
- 48-bit hardware addresses (e.g., 00-1A-2B-3C-4D-5E)
- Unique to each network interface
- Used for local network delivery

**Error Detection**:
- FCS uses Cyclic Redundancy Check (CRC)
- Receiving device recalculates FCS to verify data integrity
- Corrupted frames are discarded

**Type/Length Field**:
- **Type**: Identifies encapsulated protocol (0x0800 for IPv4, 0x86DD for IPv6)
- **Length**: Specifies data field size when used as length field

---

## 🎯 My Takeaways
- **Ethernet frames are the fundamental unit** of local network communication
- **Encapsulation creates a layered approach** where each layer adds specific control information
- **MAC addresses enable local delivery** while IP addresses handle global routing
- **The FCS field provides crucial error detection** to ensure data integrity
- **Frame structure is standardized** to ensure interoperability between devices
- **Understanding encapsulation helps troubleshoot** network communication issues
- **Each field in the frame serves a specific purpose** in the delivery process
- **The type field determines how the payload should be processed** by the receiving device

---


# 📘 Module 7.2: The Access Layer

## 📌 Key Concepts
- **Ethernet Switches**: Operate at Data Link Layer (Layer 2) using MAC addresses
- **MAC Address Tables**: Dynamic databases that map MAC addresses to switch ports
- **Learning Process**: Switches automatically build tables by examining source MAC addresses
- **Forwarding Decisions**: Based on destination MAC addresses in Ethernet frames
- **Filtering**: Switches send frames only to relevant ports, not all ports
- **Unknown Unicast**: Frames with unknown destinations are flooded to all ports except incoming

---

## 🔧 Technical Details

### Switch Operation Process
**1. Learning Phase:**
- Examines source MAC address of incoming frames
- Adds/updates MAC address table with [MAC Address → Port] mapping
- Entries typically timeout after 5 minutes of inactivity

**2. Forwarding Phase:**
- Examines destination MAC address of incoming frames
- **Known Unicast**: Forward only to specific port from table
- **Unknown Unicast**: Flood to all ports except incoming port
- **Broadcast**: Flood to all ports except incoming port

### MAC Address Table Building
**Initial State (Empty Table):**
Switch receives frame from H1 (MAC: AA-AA) on port Fa0/1
→ Adds entry: AA-AA → Fa0/1
**Frame to Unknown Destination:**
H1 sends to H4 (MAC: DD-DD) - DD-DD not in table
→ Floods frame to all ports except Fa0/1
→ H4 responds, revealing its location
→ Adds entry: DD-DD → Fa0/4

**Subsequent Communication:**
H1 sends to H4 again
→ Switch finds DD-DD in table mapped to Fa0/4
→ Forwards only to Fa0/4 (no flooding)

### Switch Benefits Over Hubs
- **Intelligent Forwarding**: Sends frames only where needed
- **Collision Reduction**: Each port is separate collision domain
- **Security**: Devices don't see traffic not intended for them
- **Performance**: Simultaneous communications on different ports

---

## 🎯 My Takeaways
- **Switches learn network topology automatically** by observing traffic patterns
- **MAC address tables enable efficient forwarding** instead of wasteful flooding
- **The learning process is continuous** - switches constantly update their knowledge
- **Unknown destinations trigger flooding** until the path is discovered
- **Switches operate transparently** - devices don't need configuration to work with switches
- **Each switch port is an independent connection** allowing simultaneous communications
- **Table timeouts handle device mobility** - if a device moves, the table updates automatically
- **Understanding switch operation is crucial** for network troubleshooting and design

---