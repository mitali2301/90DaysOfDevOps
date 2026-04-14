# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports
--

DNS – How Names Become IPs
 --
what happens when you type `google.com` in a browser

DNS Lookup - Your browser doesn't know what "google.com" is; it only understands IP addresses. It asks a DNS server: "What is the IP for google.com?" The server responds with something like 142.250.190.46.2.

TCP Handshake -  (The "Connection")Your computer reaches out to that IP address to establish a reliable connection. They perform a "Three-Way Handshake 

TLS Handshake (The "Security") - Since it's HTTPS, your browser and the server exchange "secret keys" to encrypt the conversation so no one can spy on your search.

HTTP Request (The "Ask") - Now that the tunnel is open and secure, your browser sends a formal request: "Please send me your homepage."
  
Server Response -  (The "Delivery")Google’s server processes the request and sends back a package of HTML, CSS, and JavaScript. Your browser then "paints" these files into the colorful page you see.
    
DNSApplication  (finding the destination) 

TCPTransport (ensuring data arrives)

IPNetwork (routing packets across the web)

HTMLApplication (the actual content)

2. What are these record types? Write one line each:

A: Maps a hostname directly to an IPv4 address (Example: google.com → 142.250.190.46).

AAAA: Maps a hostname to an IPv6 address (Example: google.com → 2607:f8b0:4005:802::200e).

CNAME: An alias that points one hostname to another hostname (Example: blog.example.com → ghs.googlehosted.com).

MX: Directs email to a specific mail server (Example: example.com → ASPMX.L.GOOGLE.COM).

NS: Lists the Name Servers that have the authority to manage the domain's records (Example: example.com → ns1.google.com).

4. Run: `dig google.com` — identify the A record and TTL from the output

A record : 199

TTL : 142.251.13.138

 <img width="473" height="30" alt="image" src="https://github.com/user-attachments/assets/9b7ff858-ee0c-4d10-be18-0132a8b92e15" />


---

IP Addressing
--

1. What is an IPv4 address? How is it structured?

IPV4 is Internet Protocol version 4 address is  a unique numerical label assigned to every device connected to network that uses internet protocol for communication.

IPV4 Address is 32 bit number 

ip addr show = command used in linux to check your IP address
--

 Difference between **public** and **private** IPs — give one example of each
 | private IP| public IP |
|------|-------------|-
| /24  | ?           | 
| /16  | ?          | 
| /28  |            |

 
 
4. What are the private IP ranges?
   - `10.x.x.x`, `172.16.x.x – 172.31.x.x`, `192.168.x.x`
5. Run: `ip addr show` — identify which of your IPs are private

---

### Task 3: CIDR & Subnetting
1. What does `/24` mean in `192.168.1.0/24`?
2. How many usable hosts in a `/24`? A `/16`? A `/28`?
3. Explain in your own words: why do we subnet?
4. Quick exercise — fill in:

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|------|-------------|-----------|--------------|
| /24  | ?           | ?         | ?            |
| /16  | ?           | ?         | ?            |
| /28  | ?           | ?         | ?            |

---

### Task 4: Ports – The Doors to Services
1. What is a port? Why do we need them?
2. Document these common ports:

| Port | Service |
|------|---------|
| 22   | ?       |
| 80   | ?       |
| 443  | ?       |
| 53   | ?       |
| 3306 | ?       |
| 6379 | ?       |
| 27017| ?       |

3. Run `ss -tulpn` — match at least 2 listening ports to their services

---

### Task 5: Putting It Together
Answer in 2–3 lines each:
- You run `curl http://myapp.com:8080` — what networking concepts from today are involved?
- Your app can't reach a database at `10.0.1.50:3306` — what would you check first?

---

## Documentation

Create `day-15-networking-concepts.md` with:
- Your answers to each task
- Command outputs from `dig` and `ss`
- The filled CIDR table
- What you learned (3 key points)

---

