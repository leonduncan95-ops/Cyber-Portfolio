# Wireshark Traffic Lab (DNS + ICMP + HTTP + TLS)

## One-line summary
Captured and analyzed real network traffic with Wireshark, then used display filters and built-in stats to identify DNS lookups, ICMP pings, cleartext HTTP requests, and encrypted TLS traffic.

---

## Tools used
- Wireshark (Windows)
- Web browser + `ping` (to generate traffic)

---

## What I did 
1. **Captured live traffic** on my active network interface (Wi-Fi)
2. **Used display filters** to isolate specific protocols (DNS, ICMP, HTTP, TLS)
3. **Validated what was happening** (ex: DNS queries/responses, ping requests/replies)
4. **Inspected an HTTP conversation** and used **Follow TCP Stream** to view the request/response
5. Used **Protocol Hierarchy** + **Conversations** to summarize the capture and find the “top talkers”

---

## Why this matters
In a SOC / analyst role, packet captures help you answer questions like:
- “What domain did this host query?”
- “Did the host successfully reach an external IP?”
- “Is this traffic encrypted (TLS) or cleartext (HTTP)?”
- “Who is this machine talking to the most?”

---

## Key filters I used (and why)
- `dns` — isolate domain lookups and DNS responses  
- `icmp` — confirm ping request/reply behavior  
- `http` — find cleartext web requests (useful for investigations)  
- `tls` — identify encrypted traffic (common on port 443)  
- `tcp.stream eq 12` — isolate one conversation/flow for easier inspection

---

## Evidence / screenshots

### 1) Capture running (baseline traffic)
This shows the live capture in progress (background traffic like mDNS/IGMP is normal on many networks).
![captured traffic](./captured-network-traffic.png)

---

### 2) DNS traffic (domain lookups)
Filtered to `dns` to view queries/responses. This is useful for answering “what domains did this host request?”
![dns filter](./dns-filter.png)

What I noticed:
- DNS uses **UDP/53** in many cases
- You can often see returned **A/AAAA records** and sometimes **CNAMEs**

---

### 3) ICMP traffic (ping)
Filtered to `icmp` to validate ping activity (request + reply). Helpful for connectivity checks.
![icmp filter](./icmp-filter.png)

---

### 4) HTTP traffic (cleartext web request)
Filtered to `http` to find a plain HTTP request/response.
![http filter](./http-filter.png)

---

### 5) Follow TCP Stream (reconstruct the conversation)
Used **Follow → TCP Stream** to view the request/response for the selected flow.
![follow tcp stream](./follow-tcp-stream.png)

Why this is important:
- It reconstructs what was said over the connection (when it’s not encrypted)
- Great for investigating suspicious downloads, beaconing, or data exfil in cleartext traffic

---

### 6) TLS traffic (encrypted)
Filtered to `tls` to show encrypted sessions. You can see metadata, but not the plaintext content.
![tls filter](./tls-filter.png)

---

### 7) Protocol Hierarchy Statistics (what protocols dominate)
Used **Statistics → Protocol Hierarchy** to summarize the capture.
![protocol hierarchy](./hierarchy-statistics.png)

What I noticed:
- Most traffic was **TCP/TLS** (normal for modern browsing)
- A smaller portion was **UDP/QUIC** and other background traffic

---

### 8) Conversations (top talkers)
Used **Statistics → Conversations** to see which IPs/ports had the most activity.
![conversations](./conversations.png)

Why this is useful:
- Quickly spot unusual external connections
- Identify the “main destinations” and where to investigate first

---

## Notes on privacy
I did **not** upload the full `.pcapng` file to my portfolio because packet captures can contain sensitive data. Screenshots provide proof of work without exposing private traffic.

---

## Next improvements (optional)
- Capture again using a short time window + only the traffic you generate
- Create a second lab focusing on:
  - DNS tunneling indicators
  - Suspicious HTTP user-agents / odd URIs
  - TLS SNI / certificate inspection
  - Detecting port scans in a capture

