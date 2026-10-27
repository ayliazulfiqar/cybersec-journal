# Day 21: Project 2, Session 1 (Port Scanner v1)

## What I did
- Built the first version of my Python TCP port scanner.
- Scanned TCP ports 1–1024 on my Metasploitable lab machine.
- Compared my Python scanner's results with Nmap.
- Confirmed that both tools identified the same 12 open ports: 21, 22, 23, 25, 53, 80, 111, 139, 445, 512, 513, and 514.

## Project link
👉 [Project 2: Python Port Scanner](port-scanner/README.md)

## What I learned
- I learned how Python sockets, `connect_ex()`, and loops can be used to scan TCP ports.
- I learned how to compare my scanner's results with Nmap to check its accuracy.

## Next
- **v2:** Add threading to scan ports faster and banner grabbing to collect information about services running on open ports.
