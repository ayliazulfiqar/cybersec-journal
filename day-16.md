# Day 17 - Project 1, Session 2 — Isolated Lab Network

## What I did today

- Configured a host-only network (`vboxnet0`) in VirtualBox.
- Set up Kali Linux with NAT and host-only adapters, and Metasploitable 2 with a host-only adapter.
- Checked the IP addresses of both virtual machines:
  - Kali Linux: `192.168.56.103`
  - Metasploitable 2: `192.168.56.102`
- Tested network isolation. Metasploitable returned `Network is unreachable` when I tried to ping `8.8.8.8`.
- Ran an extended Nmap scan against the target using `nmap -sV -sC -p-`.
- Found 29 open TCP ports and identified several services, including FTP, SSH, Telnet, HTTP, Samba, MySQL, and PostgreSQL.
- Saved the extended scan results to `full-scan.txt`.

## Project Link

[Project 1: Home Hacking Lab]([home-lab/README.md](https://github.com/ayliazulfiqar/home-lab))
 
## What went well

- I successfully configured the lab network and identified both machines' IP addresses.
- Nmap confirmed that the target was up and helped me discover its open ports and service versions.
- I identified potentially risky services, including anonymous FTP access, unencrypted Telnet, and an outdated Apache web server.

## Problems I hit

- I needed to understand the difference between NAT and host-only networking in VirtualBox.
- The target returned `Network is unreachable` when pinging `8.8.8.8`. This showed that it had no available route to that destination.
- The full Nmap scan took approximately 153 seconds because it checked all 65,535 TCP ports.

## What I learned

I learned how to configure an isolated virtual lab, check IP addresses, and scan a target using Nmap. I also learned that open ports and outdated services can reveal potential security risks that need further investigation.

## Next

- Confirm that clean-baseline snapshots exist for both VMs.
- Save screenshots of the IP addresses, connectivity tests, and Nmap results.
- If not already completed, capture the scan traffic in Wireshark and save the capture file.
- Continue with DVWA web application testing and learn how to inspect HTTP requests using Burp Suite.

