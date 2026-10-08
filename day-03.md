# Day 3 — Nmap & Reconnaissance

## What is Nmap?

Nmap (Network Mapper). It is a network scanning tool used to discover open ports, hosts, services, and sometimes operating systems.

## Nmap Cheat Sheet

nmap <target> - basic

nmap -sn <target> - host discovery

nmap -sT <target> - TCP connect scan

nmap -sS <target> - SYN scan

nmap -p 22,80,443 <target> - specify ports

nmap -p- <target> - scan all TCP ports

nmap -sV <target> - service/version detection

nmap -O <target> - OS detection

nmap -A <target> - aggressive detection

nmap -oN scan.txt <target> - save normal output

# My Scan 

## Scan #1 — Basic Nmap Scan

Command

nmap [TARGET-IP]

Purpose

This was my basic Nmap scan. I used it to quickly identify which common TCP ports were open on the target.

Results
PORT     STATE SERVICE
22/tcp   open  ssh
8080/tcp open  http-proxy
8081/tcp open  blackice-icecap

The host was up, and Nmap found 3 open TCP ports.

Port	State	Nmap Service Name
22	Open	SSH
8080	Open	HTTP proxy
8081	Open	blackice-icecap
Analysis

The basic scan identified three open ports: 22, 8080, and 8081.

Port 22 is identified as SSH, which is commonly used for remote administration.

Ports 8080 and 8081 were also open, but the service names shown by a basic Nmap scan should not automatically be treated as confirmed software identification. Nmap's basic scan does not perform detailed service/version detection.

For example, the blackice-icecap label on port 8081 does not prove that BlackICE is actually running. It is a service name associated with that port in Nmap's service database.

## Scan #2 — Service and Version Detection

Command

nmap -sV -p- [TARGET-IP]

Purpose

I used -p- to scan all 65,535 TCP ports and -sV to identify the services and versions running on open ports.

Results

The host was up and responded very quickly.

Three TCP ports were open:

Port	Service	Version / Information
22/tcp	SSH	OpenSSH 9.6p1 Ubuntu 3ubuntu13.19
8080/tcp	HTTP proxy?	Nmap could not confidently identify the service
8081/tcp	HTTP	Golang net/http server; possibly Go-IPFS JSON-RPC or InfluxDB API

Nmap identified the operating system as Linux.

Analysis

Port 22 is running SSH using OpenSSH 9.6p1 on Ubuntu. SSH is commonly used for remote administration.

Port 8080 was detected as http-proxy?. The? indicates that Nmap was not completely confident about the service identification, so I would investigate this port manually rather than assuming it is a proxy.

Port 8081 is running an HTTP server based on Go's net/http package. Nmap suggested that it could potentially be related to a Go-IPFS JSON-RPC service or an InfluxDB API, but this identification should be verified.

The most interesting ports to investigate further are 8080 and 8081 because they expose HTTP-based services that may provide additional information through their responses or web interfaces.

Scan #3 — SYN Scan

Command

sudo nmap -sS [TARGET-IP]

Purpose

I used -sS to perform a TCP SYN scan.

A SYN scan sends a TCP SYN packet to a port and analyses the response to determine whether the port is open, without completing the normal TCP connection.

Results
PORT     STATE SERVICE
22/tcp   open  ssh
8080/tcp open  http-proxy
8081/tcp open  blackice-icecap

Nmap found the same 3 open TCP ports:

22/tcp → SSH
8080/tcp → HTTP proxy
8081/tcp → blackice-icecap

If the target responds with SYN/ACK, Nmap can determine that the port is open.

Nmap then sends a RST instead of completing the normal TCP connection.

## Comparison With a TCP Connect Scan

A TCP connect scan (-sT) completes the TCP connection:

SYN

↓

SYN/ACK

↓

ACK

A SYN scan (-sS) does not complete the connection:

SYN

↓

SYN/ACK

↓

RST

Therefore, -sS is commonly called a half-open SYN scan.

## Comparison With My Basic Scan

My basic scan:

nmap [TARGET-IP]

and my SYN scan:

sudo nmap -sS [TARGET-IP]

found the same open ports.

However, the scans use different techniques. The basic scan uses Nmap's default scanning behavior, while -sS specifically performs a SYN scan.

The SYN scan completed in approximately 0.11 seconds, compared with approximately 0.13 seconds for my basic scan. The small difference is not particularly meaningful by itself.

## Key Lesson

The important thing I learned is that the scan result and the scanning technique are different concepts.

Nmap can discover the same open ports using different scanning methods.

The -sS scan is directly connected to the TCP three-way handshake I learned about previously.

## TryHackMe

I completed the Nmap Live Host Discovery Room, which is actually a lab environment. I only performed scanning against an authorised training target.

## Over The Wire

Reached level: 10-12

Level 8-9: It talks about human-readable strings and several = characters. So, I used strings and grep to solve the level

Level 9-10: Used the base64 command to encode data

Level 10-11: It talks about all lowercase (a-z) and uppercase (A-Z) letters being rotated by 13 positions. So I used tr "A-Za-z" 'N-ZA-Mn-za-m'
