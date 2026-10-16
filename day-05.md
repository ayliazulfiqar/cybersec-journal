# Day - 05 Reinforcing networking: TCP handshake in Wireshark

What is the difference between an IP address and a MAC address?

A MAC address is a permanent, physical, hardware-based identifier for a device on a local network. In contrast, an IP address is a temporary, assigned numerical identifier used to route data over the internet.

What does a port number do?

The port number is a virtual door that directs the incoming data to the right application or service running on the device.

What are the three steps of the TCP handshake?

The three steps of the TCP handshake are:

• SYN: The client sends a request to the server to establish a connection. 

• SYN/ACK: The server accepts the request and sends an acknowledgement back, while also asking to connect to the client.

• ACK: The client acknowledges receipt of the server's response. This final confirmation officially opens the connection.

Why does DNS use UDP?

DNS uses UDP because queries are tiny, and the request-response is simple, making delivery faster.

What does ARP do, and when is it needed?

ARP finds the MAC address of an assigned IP over a local network. It is needed when a device knows a destination IP but needs its MAC address to send the data. Once found, the device saves it to its ARP cache.

## The 6 steps website story (in my words)

When we load a website webpage, it gives an instant response, but behind the scenes it performs 6 steps with different networking protocols.

• Step 1: Getting an Identity (DHCP) 
Before you even type a URL, your machine needs a logical identity so the internet knows where to send data. When you connect to Wi-Fi, the router uses a protocol called DHCP to automatically assign your machine a unique IP address.

• Step 2: Finding the Local Exit (ARP) 
To send any request to the internet, your machine must first send it to your local router. Your machine knows the router’s IP, but local networks talk using physical MAC addresses. Your machine broadcasts an ARP request: "Who has this IP? Tell me your MAC address!" The router replies with its MAC address, which your machine saves in its ARP cache so it doesn't have to ask again.

• Step 3: Translating the Name (DNS over UDP) 
Computers don't understand names like google.com; they only understand numbers (IP addresses). Your machine sends a DNS request to look up the website's IP. This request is sent using UDP because it is incredibly fast and doesn't require a complex connection setup.

• Step 4: The Digital Handshake (TCP 3-Way Handshake) 
Now that your machine knows the website's IP, it establishes a reliable connection using TCP. They perform a 3-way handshake:

	1. SYN: Your machine asks the server to open a connection.
  
	2. SYN-ACK: The server agrees and asks to open its side of the connection.
  
	3. ACK: Your machine confirms, and the secure highway is ready.
  
• Step 5: Delivering the Goods (HTTP/HTTPS Data Flow) 
This is where the real work happens. Your browser sends an HTTP/HTTPS GET request over the established TCP connection. The server responds by streaming the website files (HTML, CSS, images), and your browser renders them on your screen.

• Step 6: The Silent Inspector (ICMP) 
While you browse, ICMP runs silently in the background. It isn't used to load the webpage, but it handles network diagnostics. If a router along the way crashes or a network path breaks, ICMP sends a "Destination Unreachable" message back to your machine to report the network failure.


# Wireshark observation:

## Observation: TCP Three-Way Handshake

**Objective:** To observe the TCP three-way handshake while establishing an HTTP connection to `example.com` using the command `curl http://example.com`.

**Procedure:**  
A packet capture was started before executing the curl command in the terminal. After the connection was initiated, the capture was stopped and filtered using `ip.addr == 93.184.216.34 or tcp.port == 80` to identify the TCP packets associated with the HTTP connection.

**Observations:**

The first three TCP packets demonstrate the TCP three-way handshake:

1. **SYN:** The client sends a SYN packet to the server to initiate a TCP connection.
2. **SYN-ACK:** The server responds with a SYN-ACK packet to acknowledge the client's request and indicate that it is ready to establish the connection.
3. **ACK:** The client sends an ACK packet to acknowledge the server's response, completing the TCP three-way handshake.

| Packet | Source (Sender) | Destination (Receiver) | TCP Flag |
|---|---|---|---|
| 1 | Client IP address | Server IP address | SYN |
| 2 | Server IP address | Client IP address | SYN-ACK |
| 3 | Client IP address | Server IP address | ACK |
