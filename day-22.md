# Day 22 — Port Scanner v2

**Goal:** Make my Python port scanner faster using multithreading and identify services using banner grabbing.

### What I Did
- Used `ThreadPoolExecutor` to scan multiple ports concurrently.
- Added banner grabbing to identify services running on open ports.
- Collected and sorted results for cleaner output.
- Added HTTP `HEAD` requests for web ports.
- Compared scan speed and results with v1 and Nmap.

### Testing
- **Target:** `192.168.56.102`
- **Ports:** 1–1024
- **v1 scan time:** 0.74 seconds
- **v2 scan time:** 1.29 seconds
- **Results:** - 12 open ports found. Banners identified:
  - Port 21: 220 (vsFTPd 2.3.4)
  - Port 22: SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1
  - Port 25: 220 metasploitable.localdomain ESMTP Postfix (Ubuntu)
  - Port 80: Apache/2.2.8 (Ubuntu) with PHP/5.2.4 response headers.

### What I Learned
- Threading improves speed for network operations.
- Banner grabbing helps identify running services.
- Nmap provides more advanced service detection.
- Timeouts and error handling make the scanner more reliable.

### Next Step
Build Port Scanner v3 with `argparse`, saved scan results, and private-IP validation.

**Project:** https://github.com/ayliazulfiqar/port-scanner
