## 🔐 TLS Handshake Analysis
## 🧠 What is TLS?

TLS (Transport Layer Security) is a cryptographic protocol used to secure communication between clients and servers.
It provides:

Confidentiality (encryption)

Integrity (tamper protection)

Authentication (server & optionally client identity)

TLS is used by HTTPS, FTPS, SMTPS, VPNs, APIs, etc.

## 🧪 Capture Setup

Tool: Wireshark
Filter:
tls
To capture only handshake messages:
tls.handshake



## 🔄 TLS Handshake Flow (Modern TLS 1.2 / 1.3)
A simplified handshake looks like:

ClientHello  →  
             ← ServerHello  
             ← Certificate  
             ← ServerKeyExchange  
ClientKeyExchange →  
ChangeCipherSpec →  
Finished →  
             ← ChangeCipherSpec  
             ← Finished  




# 🔐 TLS 1.3 Handshake (QUIC) — Full Analysis

---

# 🧩 1. QUIC Initial Packet Overview

**Packet Type:** Initial
**Version:** QUIC v1
**DCID:** `fa91a3c455e8e0fe`
**SCID:** *empty*
**Packet Number:** 2

This QUIC Initial packet contains:

* Multiple **PING** frames
* Multiple **CRYPTO** frames → these deliver TLS handshake data
* **PADDING** frames to reach minimum QUIC Initial size (1200 bytes)

TLS handshake in QUIC always occurs inside **CRYPTO frames**.

---

# 🧠 2. TLS 1.3 ClientHello (Actual Values)

### 🔹 **ClientHello Summary**

* **TLS Version:** TLS 1.2 (0x0303) *(outer record layer for TLS 1.3)*
* **Supported Version:** TLS 1.3 (0x0304)
* **Random:** `f9e22cda7ae986a6024f764927d1e31d15db43594e3a176735b7f31f463de2bf`
* **Session ID:** empty

### 🔹 **Cipher Suites**

```
TLS_AES_128_GCM_SHA256 (0x1301)
TLS_AES_256_GCM_SHA384 (0x1302)
TLS_CHACHA20_POLY1305_SHA256 (0x1303)
```

### 🔹 **Compression Method**

```
null (0)
```

---

# 🧩 3. ClientHello Extensions


## ✔ supported_versions

* Supported: **TLS 1.3**

## ✔ supported_groups

```
Unknown (0x11ec)
x25519
secp256r1
secp384r1
```

## ✔ signature_algorithms

```
ecdsa_secp256r1_sha256
rsa_pss_rsae_sha256
rsa_pkcs1_sha256
ecdsa_secp384r1_sha384
rsa_pss_rsae_sha384
rsa_pkcs1_sha384
rsa_pss_rsae_sha512
rsa_pkcs1_sha512
rsa_pkcs1_sha1
```

## ✔ encrypted_client_hello (ECH)

* **ECH is enabled**
* Cipher Suite: **HKDF-SHA256 / AES-128-GCM**
* Config ID: **191**
* Encrypted Payload: present (176 bytes)

*(This means Facebook uses ECH — your SNI and most extensions are encrypted.)*

## ✔ application_layer_protocol_negotiation (ALPN)

```
h3
```

This means you are negotiating **HTTP/3**.

## ✔ key_share

Two key shares:

1. **Unknown (4588)**, 1216 bytes
2. **x25519**, 32 bytes

QUIC typically uses **x25519** for key exchange.

## ✔ server_name (SNI)

```
edge-chat.facebook.com
```

## ✔ quic_transport_parameters
* `max_datagram_frame_size`: 65536
* `initial_max_streams_bidi`: 100
* `initial_max_stream_data_bidi_remote`: 6291456
* `initial_max_stream_data_bidi_local`: 6291456
* `initial_max_data`: 15728640
* `max_udp_payload_size`: 1472
* `google_initial_rtt`: 88529 μs
* `max_idle_timeout`: 30000 ms
* ...and more (all included in capture)

---

# 🔐 4. Meaning of the Frames

QUIC replaces TCP, so TLS handshake messages travel inside **CRYPTO frames**.

### 🔹 **PING Frames**

Purpose:

* Keep the connection alive
* Verify path connectivity
* Probes RTT / handshake responsiveness

### 🔹 **CRYPTO Frames**

Contain TLS handshake messages:

* ClientHello (in Initial)
* ServerHello (in Handshake)
* EncryptedExtensions
* Certificate
* CertificateVerify
* Finished

Your packet only contains **ClientHello**, because ServerHello comes later.

# 🧠 5. TLS 1.3 Handshake Flow (QUIC)

Your capture shows the **first step** of the TLS 1.3 handshake:

### 1️⃣ ClientHello → (your packet)

Contains:

* TLS version
* Cipher suites
* Key shares
* ECH
* QUIC transport parameters
* SNI
* ALPN

### 2️⃣ ServerHello (not in this packet)

Server selects:

* A cipher suite (likely AES-128-GCM or CHACHA20)
* A key share
* Sends its own QUIC transport parameters

### 3️⃣ EncryptedExtensions

ECH handshake continues, parameters applied.

### 4️⃣ Certificate

* Server sends certificate chain
* (Hidden since TLS 1.3 encrypts this after ServerHello)

### 5️⃣ CertificateVerify

Server proves ownership of private key.

### 6️⃣ Finished

* Server finished
* Client responds Finished

### 7️⃣ Application data

Fully encrypted HTTP/3 traffic.

---

# 🏁 6. Interpretation of This Capture

This packet shows:

* A QUIC Initial handshake starting
* Facebook’s HTTP/3 connection setup
* TLS 1.3 with ECH enabled
* Multiple PING + PADDING frames for QUIC compliance
* Full ClientHello with x25519 + GREASE + ECH


## 🔍 Wireshark Filters
tls
tls.handshake
tls.record.version == "0x0303"
tls.handshake.type == 1   # ClientHello
tls.handshake.type == 2   # ServerHello
tls.handshake.type == 11  # Certificate
