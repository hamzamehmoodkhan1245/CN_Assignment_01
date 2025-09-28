# Computer Networks - Assignment 1  
**Course Code:** Comp-352  
**Semester:** 5th (Fall 2025)  

---

## Task 4: HTTP Analysis  

**Trace file:** `http_trace.pcapng`  
**Website:** neverssl.com  

---

### Q1. What is the name of the website?  
- **neverssl.com**

---

### Q2. Find the packet that contains the first GET request for the website you have accessed.  
- **Packet Number:** 1296  

---

### Q3. Describe all headers and their values in this GET request message.  

GET /online HTTP/1.1
Host: freshsplendidserenepathway.neverssl.com
User-Agent: Microsoft-Delivery-Optimization/10.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,/;q=0.8,application/signed-exchange;v=b3;q=0.7
Connection: keep-alive
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/140.0.0.0 Safari/537.36
Referer: http://neverssl.com/

Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9


---

### Q4. Identify the status code in the first server response.  
- **HTTP/1.1 200 OK**

---

### Q5. How many HTTP response messages are exchanged in total?  
- **3 responses**

---

### Q6. Determine whether the connection is persistent or not. Justify with evidence from packet captures.  
- **Yes, the connection is persistent.**  
  - Evidence: The header includes `Connection: keep-alive`.  
  - Multiple HTTP requests and responses reuse the same TCP stream, without starting a new TCP handshake.  

---
