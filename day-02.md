# Day 2 — Networking Basics

## What happens when I open a website?

When I enter a website address into my browser, my computer first uses DNS to find the IP address associated with the domain name. After getting the IP address, my computer establishes a connection with the web server.
For a TCP connection, this begins with the three-way handshake: SYN, SYN-ACK, and ACK. The browser can then communicate with the server using HTTP or HTTPS. With HTTPS, the communication is encrypted using TLS. The server sends the requested webpage data back to my computer, and the
browser processes the HTML, CSS, JavaScript, images, and other resources needed to display the webpage.

You type:

example.com

     ↓

DNS
"What IP address is example.com?"

     ↓

IP address

     ↓

TCP connection
SYN → SYN/ACK → ACK

     ↓

HTTP/HTTPS
"Give me the webpage."

     ↓

Web server responds

     ↓

Browser receives data

     ↓

Page appears

## Common Network Ports

| Port | Protocol/Service | Purpose |
|------|------------------|---------|
| 21 | FTP | File Transfer Protocol |
| 22 | SSH | Secure remote access |
| 23 | Telnet | Remote access (unencrypted) |
| 25 | SMTP | Sending email |
| 53 | DNS | Domain name resolution |
| 80 | HTTP | Web traffic |
| 443 | HTTPS | Encrypted web traffic |
| 445 | SMB | File/printer sharing |
| 3389 | RDP | Remote Desktop |

## Network Commands

### `ip a`

I used `ip a` to inspect my network interfaces.

I also saw the loopback interface `lo`, which uses `127.0.0.1`.
There were also virtual interfaces related to Docker and OpenFaaS.

### `ping`

I used `ping` to test connectivity to another host and observe the
response time.

### `traceroute` / `tracepath`

This command shows the network hops between my computer and a destination.

### `nslookup` / `dig`

These commands allow me to query DNS and see information about domain
names and their associated IP addresses.

### `ss -tuln`

This command shows listening TCP and UDP sockets on my computer.

## Wireshark Observations

I used Wireshark to capture network traffic from my own computer.

### DNS

I used the filter:

`dns`

I observed DNS packets when my computer looked up domain information.
This helped me see that DNS is used to translate domain names into
network addresses.

### TCP

I used the filter:

`tcp.flags.syn==1`

I observed TCP connection packets and learned that TCP connections begin
with a three-way handshake involving SYN, SYN-ACK, and ACK.

### HTTP/HTTPS

I observed web-related network traffic while loading a website.
HTTPS traffic is encrypted, so the contents of the communication are
not normally visible as readable webpage data in Wireshark.

## 0SI Model 

## TryHackMe

Completed Pre Security-Network Fundamentals. 
What is Networking? and Intro to LAN. Both rooms.
# What I learned 
I learned about ping(ICMP)

Also learned about Network Topologies: A network topology defines both the physical layout of the cables and devices, and the logical way data travels through the network.

1. Star Topology: All endpoint nodes are connected directly to a single central node, typically a Layer 2 switch or hub. Data transmissions from any node must pass through the central device before reaching the destination. A link failure only isolates that specific node, but a failure of the central device causes a complete network outage.

2. Ring Topology:  Each node connects to exactly two neighbouring nodes, forming a continuous closed loop. Data frames travel sequentially from node to node in a single direction (or bidirectionally in dual-ring setups). Each node acts as a repeater to regenerate the signal. A failure of any single node or cable break disrupts the entire transmission path unless a self-healing protocol is used.

3. Bus Topology: All network devices connect to a single central coaxial cable known as the backbone or bus. Terminators are required at both ends of the cable to prevent signal reflection. Data is broadcast to all nodes simultaneously, but only the node matching the destination address processes it. A break anywhere on the backbone cable drops the entire network.

Switch: A Layer 2 (Data Link Layer) device that forwards data frames based on hardware physical addresses (MAC addresses). It populates a MAC address table by inspecting incoming frames. Instead of broadcasting data to all ports, it establishes a temporary point-to-point circuit to forward the frame exclusively to the designated destination port, minimising packet collisions

Router: A Layer 3 (Network Layer) device that routes data packets between distinct, separate networks. It evaluates network traffic using logical addresses (IP addresses) and consults its routing table to determine the optimal next-hop path across networks to forward data.

ARP: ARP operates at the interface between Layer 2 and Layer 3. It is responsible for mapping a known IP address (logical network address) to an unknown physical hardware MAC address within a local area network (LAN)

How it works:

1. Cache Check: Before encapsulating an IP packet into an Ethernet frame, a host checks its local RAM table (the ARP Cache). If the matching destination MAC address is already listed, data transmission begins immediately.

2. The Broadcast Request: If the MAC address is absent from the cache, the source host halts transmission and constructs an ARP Request packet. This packet is placed inside an Ethernet frame with the destination broadcast MAC address set to FF:FF:FF:FF:FF:FF, forcing the switch to flood it to all active ports.

3. The Unicast Reply: Every host on the local segment processes the broadcast. Hosts whose IP address does not match discard the frame. The target host, identifying its own IP address, constructs an ARP Reply packet. This response contains its physical MAC address and is sent as a direct unicast frame back to the source host.

4. Update and Transmission: The initiating host receives the reply, extracts the MAC address, logs the IP-to-MAC mapping into its ARP cache, and proceeds to encapsulate and transmit the delayed data packet.

DHCP: DHCP is a client-server protocol operating on UDP ports 67 (server) and 68 (client). It automates the distribution of IP addresses, subnet masks, default gateways, and DNS server addresses to hosts

The assignment follows a 4-step process known as the DORA cycle:

1. D - Discover: The unconfigured client broadcasts a DHCPDISCOVER packet (Destination IP 255.255.255.255) to locate available DHCP servers on the local network segment.

2. O - Offer: Any receptive DHCP server responds with a DHCPOFFER packet containing a proposed IP address from its pool, lease duration, and other configuration parameters.

3. R - Request: The client selects an offer and broadcasts a DHCPREQUEST packet. This informs the selected server it wants the address and signals unselected servers to release their offered IPs.

4. A - Acknowledgement: The chosen server logs the lease mapping and responds with a DHCPACK unicast or broadcast packet to confirm final IP allocation to the client.


## OverTheWire Bandit
Reached Level 8-9

Level 5-6: used the find command

Level 6-7: also used the find command, but with the command  2>/dev/null to silence other errors that were shown

Level 7-8: used the grep command

Level 8-9: used sort and uniq, because the hint said it was just mentioned once

## What confused me
I did every level easily, but I got confused when I saw "permission denied" on level 6-7 and then searched what I should be doing.

## What I learned

Today I learned how devices communicate over networks, how IP addresses
and ports work, what DNS does, and how TCP establishes connections. I
also used Wireshark to observe real network traffic instead of only
learning the concepts theoretically.

## Challenge: Why is HTTP less secure than HTTPS?

HTTP does not encrypt the data being transmitted. Someone able
to intercept HTTP traffic may be able to read information being sent
between the browser and the server. HTTPS uses encryption through TLS,
which helps protect the confidentiality and integrity of the
communication.
