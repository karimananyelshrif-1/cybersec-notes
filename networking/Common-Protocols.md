# 🌐 Common Network Protocols

This document summarizes the most common networking protocols used in Cyber Security and HTB Academy.

---

# TCP (Transmission Control Protocol)

## Overview

TCP is a **connection-oriented** protocol that establishes a connection before transmitting data.

### Features

- Reliable
- Ordered Delivery
- Error Checking
- Three-Way Handshake

### Common TCP Protocols

| Protocol | Port | Description |
|----------|-----:|-------------|
| SSH | 22 | Secure Remote Login |
| Telnet | 23 | Remote Login |
| HTTP | 80 | Web Traffic |
| HTTPS | 443 | Secure Web Traffic |
| FTP | 20/21 | File Transfer |
| SMTP | 25 | Send Emails |
| POP3 | 110 | Receive Emails |
| IMAP | 143 | Access Emails |
| SMB | 445 | File Sharing |
| LDAP | 389 | Directory Services |
| Kerberos | 88 | Authentication |
| RDP | 3389 | Remote Desktop |

---

# UDP (User Datagram Protocol)

## Overview

UDP is a **connectionless** protocol that sends packets without establishing a connection.

### Features

- Fast
- Lightweight
- No Delivery Guarantee
- Low Overhead

### Common UDP Protocols

| Protocol | Port | Description |
|----------|-----:|-------------|
| DNS | 53 | Domain Name Resolution |
| DHCP | 67/68 | Dynamic IP Assignment |
| TFTP | 69 | File Transfer |
| NTP | 123 | Time Synchronization |
| SNMP | 161 | Network Management |
| RIP | 520 | Routing |
| IKE | 500 | VPN Key Exchange |
| Syslog | 514 | Log Collection |

---

# ICMP (Internet Control Message Protocol)

## Purpose

Used for:

- Ping
- Error Reporting
- Network Diagnostics

### Common Messages

- Echo Request
- Echo Reply
- Destination Unreachable
- Redirect
- Time Exceeded

---

# TTL (Time To Live)

TTL decreases by **1** every time the packet passes through a router.

When TTL reaches **0**, the router drops the packet and sends an ICMP Time Exceeded message.

Typical default values:

| Operating System | TTL |
|-----------------|----:|
| Linux | 64 |
| macOS | 64 |
| Windows | 128 |
| Solaris | 255 |

---

# VoIP (Voice over IP)

Voice communication over IP networks instead of traditional telephone systems.

---

# SIP (Session Initiation Protocol)

Default Ports:

- TCP/5060
- TCP/5061

- IPsec
- NAT
