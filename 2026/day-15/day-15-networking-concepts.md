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

| Public IP | Private IP  |
|------|---------|
| Used on public Internet    | used with LAN or network |
| Recognized over internet   | Not recognized over internet      |
| Free of charge   | cost associated with its uses      |
| used in private network for internal communication | used in communication over internet     |
| 172.217.12.14 (Google) | 192.168.1.15   |

 
 
4. What are the private IP ranges?
   10.x.x.x  used in Huge Enterprises / Clouds
   
   172.16.x.x – 172.31.x.x  used in Mid-size corps / Virtualization

   192.168.x.x -  Home Wi-Fi / Small Offices
   
ip addr show  identify which of your IPs are private

private Ip -  172.31.47.255
--
<img width="659" height="224" alt="image" src="https://github.com/user-attachments/assets/9cc6882c-7063-472f-b9a9-03622ecc9443" />


 CIDR & Subnetting
 --
1. What does `/24` mean in `192.168.1.0/24`?

/24 is called CIDR notation classless inter domain routing. It tells you exactly how much of the IP address belongs to the Network and how much is available for Hosts (devices).

 How many usable hosts in a `/24`? A `/16`? A `/28`?
  /24  254 
  
  /28 = 14
  
  /16 = 65,534
  
4. Explain in your own words: why do we subnet?

is the process of dividing a large physical network into smaller, manageable logical subnetworks (subnets) to improve performance, security, and IP address efficiency

6. Quick exercise — fill in:

| CIDR | Subnet Mask | Total IPs | Usable Hosts |
|------|-------------|-----------|--------------|
| /24  | 255.255.255.0          |  256        |  254      |
| /16  | 255.255.0.0   |  65,536    | 65.534      |
| /28  | 255.255.255.240     |  16       |  14         |


 Ports – The Doors to Services
 
1. What is a port? Why do we need them?

A port is a 16-bit number (ranging from 0 to 65535) used by the Transport Layer (Layer 4) to identify a specific process or service on a device.

3. Document these common ports:

| Port | Service |
|------|---------|
| 22   | SSH     |
| 80   | HTTP      |
| 443  | HTTPS      |
| 53   | DNS     |
| 3306 | MYSQL     |
| 6379 | REDIS     |
| 27017| MongoDB       |

3. Run `ss -tulpn` — match at least 2 listening ports to their services

Two service are there port 80 and 22

<img width="1267" height="330" alt="image" src="https://github.com/user-attachments/assets/b7d698ad-a6df-4901-9402-b664000ce18d" />




- You run `curl http://myapp.com:8080`

- protocol http:// - tell curl to use hypertext transfer protocol

host myapp.com = curl first contacts your DNS resolver to find the A Record (IPv4) or AAAA Record (IPv6) for this domain.

The Port (:8080): By default, HTTP uses Port 80. By adding :8080, you are telling the computer to send the packet to a specific custom service (like a Java, Node.js, or Python app) 

--
  
Your app can't reach a database at `10.0.1.50:3306` — what would you check first?

ping to check network connectivity

 is port 3306 open

ss -tulpn | grep :3306


---





