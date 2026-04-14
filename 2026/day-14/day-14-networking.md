# Day 14 – Networking Fundamentals & Hands-on Checks

OSI layers- Open system interconnection  has 7 layers
Physical layer = Hardware, cable and eiectrical signal

Data-link layer = handles physical addressing on same local network. ipconfig

Network layer = handles routing and logical addressing. Ping / traceroute

Transport layer = handles host to host communication and data integrity

Session layer = manages the conversation between systems

Presentation layer = translates data into a format that application can understand SSL/TLS

Application layer = user interact with software
--

TCP/IP stack
 --
The TCP/IP Stack, also known as the Internet Protocol Suite, is the conceptual model and set of communications protocols used to power the internet and similar computer networks There are 4 layers in TCP/IP Stack

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


|   Protocol  |       Layer      |
|--------------|------------------|
|     IP       |  Internet Layer  |
|  TCP/UDP     |  Transport Layer |
| HTTP,HTTPS,DNS|  Application Layer|

---

#### One real example: `curl https://example.com` = App layer over TCP over IP

- Layer 7 (Application): curl creates the HTTP request (GET /index.html).
- Layer 6 (Presentation): Encrypts the data with SSL/TLS (Locked box).
- Layer 5 (Session): Adds Session ID to manage the conversation.
- Layer 4 (Transport): Wraps in TCP for reliability (Port 54321 -> 443).
- Layer 3 (Network): Adds IP addressing (Src: 192.168.1.XX -> Dst: 93.184.216.XX).
- Layer 2 (Data Link): Adds MAC addresses for the local router.
- Layer 1 (Physical): Converts data to electrical signals/radio waves to travel the wire.

## Hands-on Practical Checklist On AWS EC2
--

hostname -I  or ip addr show  = It will show your machines IP.EC2 Instance IP 54.93.201.90

<img width="682" height="316" alt="image" src="https://github.com/user-attachments/assets/604b76e3-faae-4261-8833-d41965522610" />
--

Reachability: ping www.google.com 

<img width="600" height="192" alt="image" src="https://github.com/user-attachments/assets/2169b173-f005-4bfb-ad9c-a876bb4b95a2" />
--

traceroute <target> (or tracepath) — used to track the path packets

<img width="821" height="101" alt="image" src="https://github.com/user-attachments/assets/c15272a7-5a2d-4c1a-b88f-ae6151c984ba" />


Ports: ss -tulpn (or netstat -tulpn) — list one listening service and its port. Its listening on port 22 

<img width="1245" height="136" alt="image" src="https://github.com/user-attachments/assets/688bb056-1410-4acc-8810-11873de36730" />

Name resolution: dig <domain> or `nslookup <domain> — record the resolved IP.
Dns query returned the status with NOERROR. Sucessfully resolved Domain to IP google.com

<img width="678" height="362" alt="image" src="https://github.com/user-attachments/assets/89f2a2f4-e73e-4efd-a3c1-6c63846bcb39" />


HTTP check: curl -I <http/https-url> — note the HTTP status code.
status code 200 OK. 
<img width="1352" height="190" alt="image" src="https://github.com/user-attachments/assets/9a72a9f4-660b-42a7-b8df-cf6c5e9a08ed" />

--

1) Identify one listening port from `ss -tulpn taking port 22
  
 <img width="997" height="60" alt="image" src="https://github.com/user-attachments/assets/c8f138f4-2178-43f8-bec9-4f3f61dcf57e" />

curl -I http://localhost:<port>

 
<img width="401" height="134" alt="image" src="https://github.com/user-attachments/assets/46e4e5a8-c200-46c5-8041-1f476c2c02cd" />

Next steps would be checking service status (systemctl status ssh) or firewall rules.
---


## Reflection 
- Which command gives you the fastest signal when something is broken Ping command

- What layer (OSI/TCP-IP) would you inspect next if DNS fails -
-   TCP/IP : Application layer

-   OSI Model 7 Application Layer
-   DNS is an Application Layer service that relies on the Network Layer to function
-   Common issues are invalid records , DNS Sservice layer.
-   
-
   If HTTP 500 shows up
    TCP/IP : Application layer

-   OSI Model 7 Application Layer

   HTTP 500 indicates a server-side,application error,not a network issue

   --

   Two follow-up checks you’d run in a real incident:
   --
   Two follow-up checks you’d run in a real incident:

DNS Troubleshooting
cat /etc/resolv.conf
dig google.com
<img width="607" height="247" alt="image" src="https://github.com/user-attachments/assets/5ade4154-c6a8-4033-b599-fa37dc1a070a" />

HTTP 500

tail -f /var/log/httpd/error.log

systemctl status httpd 

<img width="1048" height="101" alt="image" src="https://github.com/user-attachments/assets/2177a880-6e67-4fc1-b485-4e3eb3e1e6da" />






   
  


---

