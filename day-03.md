# Day 3 — Nmap & Reconnaissance

## What is Nmap?

Nmap (Network Mapper). It is a network scanning tool used to discover open ports, hosts, services, and sometimes operating systems.

nmap <target>

nmap -sn <target>

nmap -sT <target>

nmap -sS <target>

nmap -p 22,80,443 <target>

nmap -p- <target>

nmap -sV <target>

nmap -O <target>

nmap -A <target>

nmap -oN scan.txt <target>



## Over The Wire

Reached level: 10-12

Level 8-9: It talks about human-readable strings and several = characters. So, I used strings and grep to solve the level

Level 9-10: Used the base64 command to encode data

Level 10-11: It talks about all lowercase (a-z) and uppercase (A-Z) letters being rotated by 13 positions. So I used tr "A-Za-z" 'N-ZA-Mn-za-m'
