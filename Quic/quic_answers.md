# Task 6: QUIC-Based Website Access Analysis

This document provides an analysis of QUIC-based website access using Wireshark.  
The target website under investigation is **Google.com**.

---

## 1. Website Name
- **Google.com**

---

## 2. QUIC Initial Handshake
- The Initial QUIC handshake is carried in the **first QUIC Initial packet (Packet #1)**.  
- Information exchanged:
  - **Client → Server:** TLS 1.3 `ClientHello` (supported QUIC/TLS versions, cipher suites, Server Name Indication (SNI), key share, random values).  
  - **Server → Client:** TLS 1.3 `ServerHello` (chosen version, cipher suite, cryptographic keys).

---

## 3. TLS ClientHello inside QUIC
- The **TLS ClientHello** is found in the **very first QUIC Initial packet (Packet #1, client → server)**.  
- How to locate in Wireshark:
  - Apply the filter: `quic`
  - Locate the first “QUIC Initial” packet
  - Expand details → `TLSv1.3 Handshake Protocol` → `ClientHello`

- Information contained in `ClientHello`:
  - Supported QUIC/TLS versions
  - Cipher suites
  - Server Name Indication (SNI)
  - Key share and cryptographic parameters  

This is the first step in establishing the QUIC handshake.

---

## 4. QUIC Version
- The QUIC version used in the trace is:  
  **QUIC v1 (IETF, 0x00000001)**

---

## 5. First Use of 0-RTT or 1-RTT Keys
- **Packet #12** is the first packet using **1-RTT (application) keys**, shown as `Protected Payload (KP0)`.  
- No **0-RTT (early_data)** packets are present in this trace.

---

## 6. First Application Data (HTTP/3)
- The first packet carrying **application data (HTTP/3)** is also **Packet #12**, the first 1-RTT Protected Payload after the handshake.  
- Wireshark shows **HTTP/3 frames** inside (e.g., `HEADERS` and `DATA`).

### Difference from HTTP over TCP:
- **HTTP/3 over QUIC (UDP):**
  - Runs on QUIC (UDP-based) with built-in TLS 1.3.
  - Allows sending application data immediately after the initial handshake.
  - Reduces connection setup time and latency.
- **HTTP/1.1 or HTTP/2 over TCP:**
  - Requires a separate **TCP handshake + TLS handshake** before sending application data.
  - Adds additional round-trip delay.

---

## Summary
- **Website:** Google.com  
- **Handshake:** TLS 1.3 over QUIC Initial packet  
- **QUIC Version:** v1 (0x00000001)  
- **First 1-RTT Packet:** Packet #12  
- **First HTTP/3 Data:** Packet #12  
- **Key Difference:** HTTP/3 (QUIC) enables faster, secure connections compared to HTTP over TCP.

---

📌 *End of Task 6 Report*
