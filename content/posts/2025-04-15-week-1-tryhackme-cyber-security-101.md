---
title: Week 1 – TryHackMe - Cyber Security 101
date: 2026-04-13
layout: post
draft: true
---

## Overview

I’m two days into my cybersecurity learning shift — and deep in TryHackMe's [Cyber Security 101](https://tryhackme.com/path/outline/cyber-security-101) pathway. So far, I’ve finished:

- Introduction to Cyber Security
- Pre-Security
- Linux Fundamentals (1-3)
  - Exploring more of what I already know
- Windows Fundamentals (1–3)
  - Active Directory Basics - Boring
- Networking Concepts
  - ISO OSI model and layers
  - TCP/UDP
  - Ethernet, IP and TCP Protocols
- Networking Essentials
  - DHCP
  - ARP
  - NAT
  - ICMP (Ping & Traceroute)
  - Routing
  - NAT
- Networking Core Protocols
  - WHOIS
  - DNS
  - HTTP and FTP
  - SMTP, POP3 and IMAP
- Networking Secure Protocols
  - SSL/TLS
  - Securing Protocols
    - HTTP
    - HTTPS
    - SMTP
    - POP3
    - IMAP
  - Replace TELNET with SSH
  - Secure networks with VPN

I’m flying through it because it clicks — and because the systems I’ve worked with at my day job were just *asking* to be broken.

---

## What I Learned

### The Big Picture
- What “hacking” actually means in 2025 — not movie bullshit
- Difference between blue/red/purple teams
- The value of enumeration and information leakage

### Windows Internals
- How to use Event Viewer to track logins
- Group Policy basics — and how misconfigs can expose systems
- PowerShell = your new best friend (and worst enemy)

### Web + Network
- IP, DNS, traceroute, and how to see what’s *actually* happening under the hood
- Ran my first `nmap` scan and saw open ports on my own network
- Played with Burp Suite to intercept form data (and saw how weak some validation really is)

---

## Tools I Used

- **Kali Linux** -> Industry standard pentesting distro

- **Nmap** → Port scanning
- **Burp Suite** → HTTP interception and tampering
- **Wireshark** → Packet sniffing (briefly)
- **PowerShell** → Event log digging, process review

---

## What Tripped Me Up

Badly constructed rooms and questions.  It works for understanding but I have no intention of doing more than I need to with this.


- I assumed Windows logging would be clearer — instead it’s a firehose of noise
- Windows absolutely blows with it's incorehent naming of cli apps and location of settings.

---

## Reflections

* I need a notepad.
* I am simply not interested in windows at all.  I should be but I'm not.
* I would much rather break things from cli or apps than learn about windows crap.  Althoguh I need to learn this to break it later.



Even just two days in, I’m already seeing systems differently. At work, I used to take logins and server alerts at face value — now I’m wondering what they’re hiding. I’m not aiming to just learn exploits; I want to **understand the systems deeply enough to rebuild them better**.

---

## Next Goals

- Finish “Intro to Offensive Security”
- Write a bruteforce login script in Python (basic but real)
- __Setup Kali Linux VM (I’ve been using my host machine, but want separation)__

---

## Favorite Commands This Week

```bash
nmap -A 192.168.1.1
Get-EventLog -LogName Security -Newest 50
```

## Movie of the week
Hackers - Obviously
