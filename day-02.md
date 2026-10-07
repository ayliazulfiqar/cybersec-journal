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

My active Wi-Fi interface is `wlp2s0b1`, with the private IPv4 address
`192.168.100.19/24`.

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
Also learned about Network Topologies:
1. Star Topology
2. Ring Topology
3. Bus Topology
Switch:
Router:
ARP:
How it works:
DCHP:

## OverTheWire Bandit
Reached Level 8-9

Level 5-6: used find command

Level 6-7: also used the find command, but with the command  2>/dev/null to silence other errors that were shown

Level 7-8: used the grep command

Level 8-9: used sort and uniq, because that hint said it was just mentioned once

## What confused me
I did every level easily, but I got confused when I saw "permission denied" on level 6-7 and then searched what I should be doing.

## What I learned

Today I learned how devices communicate over networks, how IP addresses
and ports work, what DNS does, and how TCP establishes connections. I
also used Wireshark to observe real network traffic instead of only
learning the concepts theoretically.

## Challenge: Why is HTTP less secure than HTTPS?

HTTP does not encrypt the data being transmitted. Someone who is able
to intercept HTTP traffic may be able to read information being sent
between the browser and the server. HTTPS uses encryption through TLS,
which helps protect the confidentiality and integrity of the
communication.
