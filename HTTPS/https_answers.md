# HTTPS Packet Analysis – Assignment Report

This document contains the analysis of captured HTTPS packets from **www.amazon.com**, covering the TLS handshake, certificate details, and encrypted application data.  

---

## Q7. Website Name
- **Answer:**  
  The website name extracted from the `server_name` extension in the ClientHello message is:  
  **`www.amazon.com`**

---

## Q8. ClientHello Packet
- **Answer:**  
  - **Packet Number:** `#370`  
  - The packet contains the **TLS ClientHello** message, which initiates the TLS handshake with the server.  
  - Key details:  
    - TLS Version (proposed): **1.2 (0x0303)**  
    - Session ID Length: **32**  
    - Cipher Suites Proposed: **16 suites**  
    - Extensions: GREASE, status_request, supported_versions, ec_point_formats, signature_algorithms, supported_groups, ALPN, key_share, etc.  

---

## Q9. TLS Extensions in ClientHello
- **Answer:**  
  The following TLS extensions were included in the ClientHello (packet #370):  

  - Reserved (GREASE)  
  - status_request (OCSP stapling)  
  - supported_versions (TLS 1.3, TLS 1.2)  
  - ec_point_formats  
  - signed_certificate_timestamp  
  - signature_algorithms  
  - compress_certificate  
  - supported_groups  
  - psk_key_exchange_modes  
  - Unknown type 17613  
  - encrypted_client_hello  
  - extended_master_secret  
  - session_ticket  
  - renegotiation_info  
  - server_name (**www.amazon.com**)  
  - application_layer_protocol_negotiation (ALPN)  
  - key_share (X25519MLKEM768, x25519)  
  - Reserved (GREASE)  

---

## Q10. ServerHello & Cipher Suite
- **Answer:**  
  - **Packet Number:** `#707`  
  - **Cipher Suite Chosen:** `TLS_AES_256_GCM_SHA384 (0x1302)`  
  - **TLS Version (legacy field):** `TLS 1.2 (0x0303)`  
  - **Note:**  
    Although the legacy version field shows `0x0303` (TLS 1.2), the `supported_versions` extension in the ServerHello indicates that the session is actually negotiated using **TLS 1.3**.

---

## Q11. Certificate Message
- **Answer:**  
  - **Packet Number:** `#2523`  
  - **Server Certificate (Certificate (0))**  
    - **Subject:** `CN=fls-na.amazon.com`  
    - **Issuer:** `CN=Amazon RSA 2048 M03, O=Amazon, C=US`  
    - **Validity:**  
      - **Not Before:** `2025-09-03 00:00:00 (UTC)`  
      - **Not After:**  `2026-10-02 23:59:59 (UTC)`  

---

## Q12. First Encrypted Application Data
- **Answer:**  
  - **Packet Number:** `#2398`  
  - **Explanation:**  
    - Packet #2398 is the **first TLS Application Data record** after the TLS handshake.  
    - The HTTP request/response (headers and body) is encapsulated inside this encrypted record.  

    **Why HTTP headers are not visible:**  
    - TLS encrypts all application data after the handshake.  
    - Wireshark can only display the TLS record layer (content type, record length, IV/nonce, ciphertext).  
    - The actual HTTP headers and payload are hidden because they are encrypted with session keys.  
    - Modern TLS (1.2 with ECDHE, or TLS 1.3) uses **ephemeral key exchanges**, so even the server’s private key is not sufficient for decryption.  
    - To decrypt, one would need access to the session secrets (e.g., via the browser’s `SSLKEYLOGFILE`).  

    **Conclusion:**  
    The absence of visible HTTP headers in packet #2398 is expected — TLS ensures confidentiality of the application data.  

---

✨ This completes the HTTPS analysis task (Q7 → Q12) with structured answers and proper formatting.  
