---
title: "How I Layered a Proxy and VPN for Ghost Mode in Kali"
date: 2025-04-23
layout: post
draft: false
---

## Introduction

In the realm of cybersecurity, maintaining anonymity and security while conducting research or penetration testing is crucial. This article explores how I established a multi-layered internet access system using **Kali Linux**, a proxy, and a VPN to achieve "ghost mode". This configuration allows me to operate invisibly online, avoiding potential risks and unwanted attention.

## Why I Did This

The core environment is a Kali Linux VM running in isolation, ensuring that any misbehaving tools or accidental leaks don’t affect the host system. To cloak the traffic, I use a Shadowsocks proxy — a lightweight, fast proxy that helps bypass deep packet inspection built in to PIA. This connects to a VPS in Country A. On top of that, PIA's VPN (configured with OpenVPN) adds an encrypted layer and exits traffic in a completely different location (Country B), creating geographic and protocol-based separation.

- **Secure Access**: To use **Kali Linux** in various environments while maintaining anonymity.
- **Avoid Exposures**: To prevent **DNS leaks**, **IP exposure**, and **traffic fingerprinting**.
- **Multi-Country Routing**: To route my internet traffic through multiple countries for added obfuscation.
- **Tool Usage**: To use tools like **Wireshark**, **Metasploit**, or **Burp Suite** without giving away my intentions.

## The Tools I Use

Here’s the technical setup I implemented:

1. **Kali Linux Virtual Machine (VM)**: My go-to environment for penetration testing.
2. **Shadowsocks Proxy**: Connected to a remote VPS in Country A.
3. **PIA VPN (Private Internet Access)**: Utilizes OpenVPN and WireGuard for secure, multi-hop routing (Country B).

## How It Works

Everything runs through PIA's built-in multihop stack:
When Kali connects to the internet, all traffic first routes through the Shadowsocks proxy, which forwards it to my VPS. This adds obfuscation, making it harder for any monitoring system to identify the actual nature of my traffic. From there, the traffic continues through the PIA VPN tunnel — which handles encryption and final exit to the public internet. Because PIA supports multi-hop, even if my VPS were compromised, it wouldn’t lead directly to me.

- **Shadowsocks**: Obfuscates traffic to make it harder to identify or block.
- **OpenVPN**: Carries this traffic to its final destination.

PIA’s multi-hop routing simplifies the configuration, eliminating the need for custom VPS setups or complex proxy configurations.

## VPN Configuration with PIA

I use OpenVPN primarily for compatibility with Shadowsocks. WireGuard, while faster, doesn’t always play nicely in layered setups without additional configuration. The kill switch ensures no traffic escapes unencrypted, and MACE provides lightweight ad and tracker blocking at the DNS level — which has proven helpful when testing tools that pull third-party resources.

- **Protocol**: OpenVPN (compatible with Shadowsocks).
- **Kill Switch**: Enabled to ensure no data is transmitted without a stable connection.
- **MACE**: Turned on to block malicious domains and ads.
- **Auto-connect**: Enabled for seamless setup when the device boots.
- **Split Tunneling**: Disabled – all traffic goes through PIA.

### CLI Configuration Options

```bash
piactl set protocol wireguard  # Configure WireGuard as the preferred protocol
piactl set killswitch auto     # Enable kill switch on boot
piactl set mace true         # Activate MACE for enhanced protection
piactl connect               # Establish a connection
```

## Verification

To confirm the setup is configured correctly I have the following in a bash script I run periodically and always on start:

```bash
piactl get connectionstate  # Check if you're connected
piactl get vpnip           # Get your current VPN IP address
piactl get region          # Confirm which country you're connected through
```
and I also check for the actual connection and potential leaks with the following:

```bash
curl https://ifconfig.me  # Check your public IP address
curl https://ipinfo.io    # Verify your internet location
dig +short myip.opendns.com @resolver1.opendns.com  # Check DNS configuration
```

I'll also monitor my communication with wireshark with the following setup.

- **TCP Stream Timeout**: 1 minute to ensure only active connections are captured.
- **MTU (Maximum Transmission Unit)**: Auto-MTU enabled to prevent fragmentation.
- **Kernel Module**: Enabled for better interface access and performance.

If the VPN drops, PIA’s kill switch automatically blocks all outbound traffic—no DNS leaks or fallback IP exposure.

## What I Learned

This setup has taught me several valuable lessons:

- **Layering Security**: Combining Shadowsocks with a robust VPN creates an undetectable connection.
- **MACE is a Game-Changer**: It blocked malicious callbacks from tools I was testing.
- **Auto-MTU Matters**: Without it, tools like Burp Suite and curl would break due to fragmented packets.
- **Single Provider = Low Maintenance**: Relying on PIA’s built-in features simplifies routing and reduces maintenance.

## Key Takeaways

- Use a VPN with built-in multi-hop routing for added security.
- Enable kill switch and MACE features to prevent leaks and block malicious traffic.
- Always verify your setup with sanity checks to ensure everything is working as intended.
- Keep it simple with a single provider for easier maintenance.

## Conclusion

This ghost mode setup is clean, portable, and works across any Kali box or travel laptop. It’s designed to stay out of sight while maintaining full functionality. By combining a proxy with a VPN, I’ve created a secure, multi-hop connection that keeps my activities undetectable and my identity hidden.

The journey into setting up this multi-layered security system has been both challenging and rewarding. It’s not perfect, but it works—and when you need stealthy internet access, sometimes simple is the best solution. I’m excited to see how others enhance this method or share their own setups in the comments below.
