# Day 04 — Network Protocols and Packet Analysis

What I learned today

MAC Address: It is the physical address or hardware address of the device

IP Address: It is a unique numerical address assigned to each device connected to the internet

Port: It is a virtual door that directs incoming data to the right app or program running on the device

## Network Protocol

## ARP

ARP (Address Resolution Protocol) finds a device's MAC address when you know its IP address on a local area network (LAN).

## ICMP 

ICMP (Internet Control Message Protocol) acts as a messaging and status-reporting protocol at the network layer, though it is more accurately described as a network diagnostic and error-reporting protocol rather than a general-purpose message provider.

## TCP HANDSHAKE

The TCP handshake is a three-step connection process that lets two devices start talking to each other. It is a unicast (one-to-one) protocol, meaning it does not broadcast messages to the whole network. Its main goal is reliability, not security—it ensures both the sender and receiver are ready and synchronized before any data is sent. True security and encryption happen later through a separate protocol, like TLS.

How it works: SYN --> SYN/ACK --> ACK

## Questions

Why does a device need ARP if it already knows the IP address?

Even though a device knows the destination IP address, it still needs ARP to find the physical MAC address of the target device. IP addresses are used for routing data across different networks globally, but physical hardware inside a local network (like switches) can only move data using MAC addresses. ARP acts as the bridge that translates the known IP address into the required MAC address so the data can actually be delivered.

Why would a gaming or video call use UDP instead of TCP?

Gaming and video calls use UDP instead of TCP because UDP prioritizes speed and real-time delivery over perfect data accuracy. TCP is a reliable protocol that forces devices to retransmit lost data, which causes noticeable lag and stuttering. UDP, on the other hand, just sends data continuously without waiting for confirmations. In a live video call or game, a tiny drop in quality (like a brief glitch or missing frame) is much better than a frozen screen caused by lag.

What does a closed port look like to Nmap, compared to an open one?

To Nmap, an open port means a service is actively running and ready to talk, allowing Nmap to probe it for software versions. A closed port means the host device is online, but it actively rejects the connection by sending back a reset signal. Because no application is listening on a closed port, Nmap cannot pull any version information from it.



## What Happens When You Load a Website: A Step-by-Step Story

Loading a website like example.com feels instant, but behind the scenes, your laptop goes through a six-step process using different networking tools to get the job done.

1. Getting an Identity (IP Assignment)

Before doing anything, your laptop needs a local identity. As soon as you connect to the Wi-Fi, your router assigns your laptop a unique IP address (like a digital home address) so other devices on the network know where to send information.

2. Translating the Name (DNS via UDP)

Computers can't read text names like example.com—they only understand numbers. Your laptop needs to look up the website's IP address. It uses DNS to ask a server for the matching numbers. Because this needs to be incredibly fast, it uses UDP, sending a quick question without any formal setup and waiting for a rapid reply.

3. Finding the Gateway (ARP)

To send that request out to the internet, your laptop has to pass it through your local router. Your laptop knows the router's IP address, but local network hardware can only talk using physical MAC addresses. Your laptop broadcasts a shout to the whole local network: "Who owns this router IP? Send me your hardware ID!" The router responds with its MAC address. This translation step is ARP.

4. The Digital Handshake (TCP)

Now that your laptop knows how to reach the outside world, it contacts the website's server. Before swapping any actual web data, they must agree to talk using a reliable connection called TCP. They perform a three-way handshake to make sure neither side drops any information:
• Your laptop says "Hello?" (SYN)
• The server replies "I hear you, do you hear me?" (SYN-ACK)
• Your laptop confirms "Yes, I do!" (ACK)

5. Passing the Data (HTTP/Data Flow)

With the secure, reliable connection officially established, the real work begins. Your laptop requests the webpage files, and the web server streams the data back, filling your browser screen with the website.

6. Checking Network Health (ICMP)

While the website runs, another protocol called ICMP works quietly in the background. It doesn't load web pages; instead, it handles network status and error reporting. If a server suddenly crashes, ICMP sends back an "unreachable" error flag. It is also the tool used when you "ping" a device to see if it is still online and alive.

## Wireshark Observation

# 1. Observation: Address Resolution Protocol (ARP)

**Objective:** To observe ARP packets and understand how a device discovers the MAC address associated with an IP address on a local network.

**Procedure:**  
The current ARP table was viewed using the `arp -a` command. The ARP cache was cleared, and the default gateway (router) was pinged. I started a Wireshark capture and applied the `arp` filter to observe ARP request and reply packets.

**Observations:**

The ARP request contains a broadcast message asking which device has a particular IP address. In Wireshark, the request appears in the following format:

- **ARP Request:** “Who has [router IP address]? Tell [client IP address].”
- **ARP Reply:** The router responds with its MAC address.

| Packet | Sender | Receiver | Purpose |
|---|---|---|---|
| ARP Request | Client device | All devices on the local network (broadcast) | Requests the MAC address of the router |
| ARP Reply | Router | Client device | Provides the router's MAC address |

# 2. Observation: Internet Control Message Protocol (ICMP)

**Objective:** To observe ICMP echo request and echo reply packets generated by the ping command.

**Procedure:**  
A packet capture was started, and a host was pinged using the `ping` command. The Wireshark display filter `icmp` was applied to identify ICMP packets.

**Observations:**

Two main types of packets were observed:

- **Echo Request:** The client sends an ICMP packet to the destination host to check connectivity.
- **Echo Reply:** The destination host responds to the request if it is reachable and configured to reply.

| Packet | Sender | Receiver | ICMP Type |
|---|---|---|---|
| 1 | Client IP address | Destination IP address | Echo Request (Type 8) |
| 2 | Destination IP address | Client IP address | Echo Reply (Type 0) |


# 3. Observation: User Datagram Protocol (UDP) and DNS

**Objective:** To observe DNS query and response packets and understand the use of UDP in DNS communication.

**Procedure:**  
Start a packet capture before performing a DNS lookup, such as opening a website or running `nslookup example.com`. The Wireshark display filter `dns` was applied to examine the DNS queries and responses.

**Observations:**

The DNS lookup typically involves the following exchange:

- **DNS Query:** The client sends a request to a DNS resolver to obtain the IP address associated with a domain name.
- **DNS Response:** The DNS resolver returns the requested DNS information, such as an IP address.

| Packet | Sender | Receiver | Protocol / Message |
|---|---|---|---|
| 1 | Client IP address | DNS resolver IP address | DNS Query over UDP |
| 2 | DNS resolver IP address | Client IP address | DNS Response over UDP |
