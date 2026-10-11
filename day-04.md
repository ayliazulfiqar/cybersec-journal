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

