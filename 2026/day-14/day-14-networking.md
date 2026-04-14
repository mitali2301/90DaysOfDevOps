# Day 14 – Networking Fundamentals & Hands-on Checks

Get comfortable with core networking concepts and the commands you’ll actually run during troubleshooti





## Quick Concepts

- OSI layers (L1–L7) vs TCP/IP stack (Link, Internet, Transport, Application)

- OSI Layers - Open system interconnection  has 7 layers

  Physical layer = Hardware, cable and eiectrical signal

  Data-link layer = handles physical addressing on same local network. ipconfig

  network layer = handles routing and logical addressing. Ping / traceroute

  Transport layer = handles host to host communication and data integrity

  session layer = manages the conversation between systems

  presentation layer = translates data into a format that application can understand SSL/TLS

  Application layer = user interact with software

  TCP/IP stack
  --
 The TCP/IP Stack, also known as the Internet Protocol Suite, is the conceptual model and set of communications protocols used to power the internet and similar computer networks

There are 4 layers in TCP/IP Stack

Application Layer - where your software sits (http https DNS FTP SSH)
 
Transport layer = end to end connection. Responsible for creating connection between source and destination. TCP/UDP

TCP = Transmission control protocol is connection oriented to ensure data delivered reliably in correct order 

UDP = User datagram protocol is connectionless. faster but does not gurantee delivery

Internet layer = handles logical handling and routing of data packets.

Network layer - deals with physical hardware IP

TCP/IP STACK VS OSI LAYERS

TCP/IP Stands for transmission control protocol and Internet protocol 
--

contains 4 layers 

protocols are not strictly defined

protocol dependent standard

protocol devloped first then model model was devloped

OSI Layers
--

stands for open system interconnection 

contains 7 layers

protocol are strictly defined

protocol indepenent standard

model was devloped first then protocol is devloped

 Where **IP**, **TCP/UDP**, **HTTP/HTTPS**, **DNS** sit in the stack
 --

HTTP/HTTPS/DNS = Application Layer
- 
- TCP/ IP = Transport Layer

- One real example: “`curl https://example.com` = App layer over TCP over IP”

---


hostname -I  or ip addr show

Reachability: ping <target> mention latency and packet loss.

<img width="754" height="253" alt="image" src="https://github.com/user-attachments/assets/40008b04-5bd5-4a87-9a7d-394c738fc5c5" />


Path: traceroute <target> (or tracepath) — note any long hops/timeouts.

<img width="821" height="101" alt="image" src="https://github.com/user-attachments/assets/c15272a7-5a2d-4c1a-b88f-ae6151c984ba" />


Ports: ss -tulpn (or netstat -tulpn) — list one listening service and its port.

<img width="1295" height="165" alt="image" src="https://github.com/user-attachments/assets/3e073a8a-84fe-40b5-990b-7ac4ff521313" />

Name resolution: dig <domain> or `nslookup <domain> — record the resolved IP.

<img width="574" height="379" alt="image" src="https://github.com/user-attachments/assets/4542384b-6231-430b-a9a0-4b301a8ae566" />

HTTP check: curl -I <http/https-url> — note the HTTP status code.
status code 200 
<img width="1352" height="190" alt="image" src="https://github.com/user-attachments/assets/9a72a9f4-660b-42a7-b8df-cf6c5e9a08ed" />



## Mini Task: Port Probe & Interpret
1) Identify one listening port from `ss -tulpn` (e.g., SSH on 22 or a local web app)
  
 <img width="997" height="60" alt="image" src="https://github.com/user-attachments/assets/c8f138f4-2178-43f8-bec9-4f3f61dcf57e" />

 From the same machine, test it: `nc -zv localhost <port>` (or `curl -I http://localhost:<port>`).  
 
 <img width="837" height="37" alt="image" src="https://github.com/user-attachments/assets/341a9795-988e-4fe9-97e7-4cce51c8bb36" />

5) Write one line: is it reachable? If not, what’s the next check? (e.g., service status, firewall).
---


## Reflection (add to your markdown)
- Which command gives you the fastest signal when something is broken?
- What layer (OSI/TCP-IP) would you inspect next if DNS fails? If HTTP 500 shows up?
- Two follow-up checks you’d run in a real incident.


---

