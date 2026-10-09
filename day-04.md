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
