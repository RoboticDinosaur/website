---
title: "[Challenge Name] – [CTF Name] Writeup"
date: YYYY-MM-DD
series: "CTF Writeups"
categories: ["Pentesting", "CTF", "[Specific Category like Web, Crypto, Pwn, etc.]"]
tags: ["CTF", "Pentest", "[Tool Used]", "[Vulnerability Type]", "[Platform if relevant]"]
author: [Your Name or Handle]
summary: "A walkthrough of the [Challenge Name] from [CTF Name], covering the approach, tools, and exploitation steps."
draft: true
---

## Overview

Briefly introduce the challenge:
- Name: **[Challenge Name]**
- Category: **[Category, e.g., Web, Pwn, Forensics]**
- Points: **[XX]**
- CTF Event: **[CTF Name, Year]**
- Description: *[Copy/paste or paraphrase the challenge description]*

---

## Enumeration

I started with an nmap scan to test for available vulnerbilities on the target device.  This was a default scan and nothing out of the normal.

```bash
nmap -sC -sV --script vuln 10.10.x.x

[...]

Host script results:
|_samba-vuln-cve-2012-1182: NT_STATUS_ACCESS_DENIED
|_smb-vuln-ms10-054: false
|_smb-vuln-ms10-061: NT_STATUS_ACCESS_DENIED
| smb-vuln-ms17-010:
|   VULNERABLE:
|   Remote Code Execution vulnerability in Microsoft SMBv1 servers (ms17-010)
|     State: VULNERABLE
|     IDs:  CVE:CVE-2017-0143
|     Risk factor: HIGH
|       A critical remote code execution vulnerability exists in Microsoft SMBv1
|        servers (ms17-010).
|
|     Disclosure date: 2017-03-14
|     References:
|       https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2017-0143
|       https://technet.microsoft.com/en-us/library/security/ms17-010.aspx
|_      https://blogs.technet.microsoft.com/msrc/2017/05/12/customer-guidance-for-wannacrypt-attacks/
```

This came back with a number of ports that where open and the, now expected, ms17-010 vulnerbility so I stopped my research here and went ahead and fired up metaploit

## Exploitation

Detail the main vulnerability or misconfiguration exploited:

* How you identified it
* Why it's exploitable
* Exploit steps (code snippets, screenshots, etc.)

As noted in the research stage,

# Example exploit snippet
import requests
payload = {"user": "admin' -- "}
r = requests.post("http://target/login", data=payload)

Privilege Escalation

If applicable, describe how you escalated privileges:

    Enumeration tools (e.g., linpeas, pspy, manual inspection)

    Exploit method

    Relevant file/content

Post-Exploitation / Flag Retrieval

    Where the flag was found

    Final thoughts on how you could’ve optimized or improved

cat /root/root.txt

Lessons Learned

What was interesting, tricky, or new:

    Mistakes or false starts

    New tools or techniques learned

    How this challenge connects to real-world pentesting

References

    [Links to relevant tools or writeups]

    [Exploit-DB, CVEs, docs, etc.]
