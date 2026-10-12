# Day 7 - Checkpoint, then Web Basics

## Networking Checkpoint

**Score: 2.5/4 (62.5%)**

1. Walk through what happens when you open a website (DNS, ARP, TCP handshake, data).

My answer:

DNS translates the domain name into an IP address, usually using UDP.

ARP resolves the MAC address of the next device on the local network, usually the router for internet traffic.

TCP establishes a connection using the three-way handshake: SYN → SYN-ACK → ACK.

The browser sends an HTTP request, and the server returns an HTTP response containing the requested data.

ICMP can be used for network diagnostics, but it is not required for normal website loading.

Score: 0.75/1

2. What does a port do? Name 5 common ones.

A port is a numbered endpoint that directs network traffic to the correct service on a device.
Port	Service
21	FTP — File Transfer Protocol
22	SSH — Secure Shell
25	SMTP — Simple Mail Transfer Protocol
53	DNS — Domain Name System
443	HTTPS — Secure Hypertext Transfer Protocol

Score: 0.5/1

3. TCP vs UDP: one difference and one use for each.

My answer:

TCP focuses on reliable and ordered data delivery, while UDP has less built-in delivery overhead and does not guarantee delivery or ordering.

    TCP use case: Web traffic using HTTP/1.1 or HTTP/2 over HTTPS.

    UDP use case: Real-time voice communication.

Score: 0.5/1

4. Which of the SYN, SYN-ACK, and ACK packets does Nmap send in a SYN scan, and what does it do next?

My answer:

Nmap sends a SYN packet to check a target port. If the port is open, the target usually responds with SYN-ACK. Nmap typically sends an RST packet to terminate the half-open connection instead of completing the three-way handshake with ACK.

Open port: SYN-ACK response.

Closed port: Usually an RST response.

Filtered port: The probe may receive no response or an ICMP error.

Nmap continues scanning the other requested ports.

Checkpoint reflection:

My main areas to improve are memorising common port numbers, explaining TCP vs UDP with examples, and understanding how Nmap identifies open and closed ports.

## How HTTP Requests and Responses Work

An HTTP request is a message sent by the client's browser to a web server asking for a resource or submitting information

An HTTP response is the server's reply. It contains a status code, response headers and sometimes a response body containing HTML, JSON, an image or other data.

**Example:**

Request: GET / HTTP/1.1 - Meaning: Request the website's homepage.

Response: HTTP/1.1 200 OK - Meaning: The request succeeded.

## Browser Developer Tools Practice

Website tested: https://google.com

Steps performed:

    Opened the website in my browser.

    Opened Developer Tools using F12.

    Selected the Network tab.

    Reloaded the page and selected a request.

    Inspected the request method, status code, and headers.

Observation:

- **Request Method:** `GET`
- **Status Code:** `200`
- **Request Headers:** `Accept 	text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8`
- **Response Headers:** `content-type 	text/html; charset=UTF-8`

<img width="1363" height="571" alt="image" src="https://github.com/user-attachments/assets/fc524e37-02ca-426b-8003-52469a1185e5" />

**What I learned:**

The browser sends an HTTP request to Google's server.

The server returns an HTTP response with a status code and response headers.

The Network tab lets me inspect requests and responses.

*_I also compared the output of the Network tab with the command_ ***curl -I https://google.com*** _; it clarified my concept by showing more details*

_ <img width="640" height="264" alt="image" src="https://github.com/user-attachments/assets/f438d3f3-1299-4358-8c3f-2632815cde58" />

## HTTP Status Codes

200 | OK                    | The request succeeded.

301 | Moved Permanently     | The resource has permanently moved to another URL.

403 | Forbidden             | The server refuses access to the requested resource.

404 | Not Found             | The requested resource could not be found.

500 | Internal Server Error | The server encountered an unexpected problem.

## TryHackMe 

1. Completed HTTP in details

2. Completed DNS in details

Notes: Learned how DNS  works and how it helps in accessing the internet; also learned how you request content from the web server using HTTP

## What I Learned Today

How DNS, ARP, TCP, and HTTP work together.

What ports are and why services use them.

The difference between TCP and UDP.

How HTTP requests and responses work.

How to inspect HTTP traffic using browser Developer Tools.
