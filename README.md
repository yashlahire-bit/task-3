# task3-EL-

## 1. Project Overview
This project fulfills the requirements for **Task 3: Networking Basics for Cyber Security**. The goal was to capture live network traffic, analyze various protocol layers, and demonstrate the difference between secure and insecure communications.

## 2. Environment & Identification
During the capture session, the following local host information was identified:
* **Local IP Address:** `192.168.0.102`.
* **MAC Address:** `50:5a:65:f6:b3:05` (AzureWave Technology).
* **Network Gateway:** `60:32:b1:08:23:ba` (TP-Link Technology).

## 3. Protocol Analysis

### A. TCP (Transmission Control Protocol)
* **Handshake & Connectivity:** Observed various TCP streams connecting to external IPs such as `13.107.9.158`.
* **Error Detection:** The capture identified network instability through **TCP Retransmissions** and **Duplicate ACKs** (e.g., packets #2671 and #2672).
* **Connection Reset:** A `[RST, ACK]` flag was observed at packet #13390, indicating a hard close of a session.

### B. HTTP vs. HTTPS (Security Observation)
* **HTTP (Plain-Text):** Using the filter `tcp.port == 80`, I successfully captured unencrypted web traffic. 
    * **Resource Captured:** `GET /acunetix-logo.png HTTP/1.1`.
    * **Vulnerability:** All headers and data are visible in plain text.
* **HTTPS/TLS (Encrypted):** Traffic to Port 443 utilized **TLSv1.2**.
    * **Observation:** Data is labeled as "Application Data" and is mathematically obscured from analysis.



## 4. Analytical Methods Used
* **Conversation Summaries:** Used the Wireshark Conversations window to identify high-traffic endpoints.
* **Stream Filtering:** Applied specific filters (`ip.addr == 13.107.9.158`) to isolate and investigate specific communication sessions.
* **Protocol Dissection:** Analyzed Ethernet, IPv4, and TCP header structures to understand data encapsulation.

## 5. Conclusion
The capture demonstrates that HTTP traffic poses a significant security risk as sensitive data (like GET requests and host information) is transmitted in cleartext. Modern security relies on TLS to ensure that "Application Data" remains confidential during transit.
