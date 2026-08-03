# 🌐 Networking Protocols

This document contains common networking protocols and technologies frequently encountered in networking, cybersecurity, and HTB Academy.

---

## IGRP (Interior Gateway Routing Protocol)

- Cisco proprietary routing protocol.
- Used for routing inside an Autonomous System (AS).
- Legacy protocol and replaced by EIGRP.

---

## EIGRP (Enhanced Interior Gateway Routing Protocol)

- Advanced Cisco routing protocol.
- Faster convergence than IGRP.
- Used in enterprise networks.

---

## PGP (Pretty Good Privacy)

- Encrypts emails and files.
- Provides confidentiality and digital signatures.

---

## NNTP (Network News Transfer Protocol)

- Used to read and distribute Usenet newsgroups.

---

## CDP (Cisco Discovery Protocol)

- Cisco proprietary discovery protocol.
- Identifies directly connected Cisco devices.
- Shows hostname, IP address, platform, and interfaces.

---

## HSRP (Hot Standby Router Protocol)

- Cisco redundancy protocol.
- Provides a backup router if the primary router fails.

---

## VRRP (Virtual Router Redundancy Protocol)

- Open standard redundancy protocol.
- Similar to HSRP but vendor-independent.

---

## STP (Spanning Tree Protocol)

- Prevents Layer 2 switching loops.
- Avoids Broadcast Storms.
- Runs on Ethernet switches.

---

## TACACS

**Terminal Access Controller Access-Control System**

- AAA protocol.
- Authentication
- Authorization
- Accounting

Used to manage administrator access to network devices.

---

## SIP (Session Initiation Protocol)

- Establishes and terminates VoIP sessions.
- Used for voice and video calls.

---

## VoIP (Voice over IP)

- Voice communication over IP networks.
- Replaces traditional telephone systems.

---

## EAP (Extensible Authentication Protocol)

- Authentication framework.
- Commonly used in:
  - Wi-Fi
  - VPN
  - 802.1X Authentication

---

## LEAP (Lightweight Extensible Authentication Protocol)

- Cisco wireless authentication protocol.
- Deprecated because of security weaknesses.

---

## PEAP (Protected Extensible Authentication Protocol)

- Secure version of EAP.
- Encrypts the authentication process.

---

## SMS (Systems Management Server)

- Microsoft management solution.
- Software deployment.
- Device management.
- Updates.

---

## MBSA (Microsoft Baseline Security Analyzer)

- Microsoft security scanner.
- Detects missing updates and security misconfigurations.

---

## SCADA (Supervisory Control and Data Acquisition)

Industrial control system used in:

- Power plants
- Water treatment
- Manufacturing
- Critical infrastructure

---

## VPN (Virtual Private Network)

- Creates an encrypted tunnel over the Internet.
- Provides secure remote access.

---

## IPsec (Internet Protocol Security)

- Encrypts IP traffic.
- Commonly used with VPNs.
- Provides confidentiality, integrity, and authentication.

---

## PPTP (Point-to-Point Tunneling Protocol)

- Legacy VPN protocol.
- Easy to configure.
- No longer considered secure.

---

## NAT (Network Address Translation)

- Translates Private IP addresses into Public IP addresses.
- Allows multiple devices to share one Public IP.

---

## CRLF (Carriage Return Line Feed)

- Indicates the end of a line.
- Used in HTTP and SMTP.
- Related to CRLF Injection attacks.

---

## AJAX (Asynchronous JavaScript and XML)

- Updates web pages without reloading them.
- Used in modern web applications.

---

## ISAPI (Internet Server Application Programming Interface)

- Extension interface for Microsoft IIS.
- Used to build high-performance web applications.

---

## URI (Uniform Resource Identifier)

- General identifier for Internet resources.

Example:

```
mailto:user@example.com
```

---

## URL (Uniform Resource Locator)

- A type of URI.
- Specifies where a resource is located.

Example:

```
https://example.com/login
```

---

## IKE (Internet Key Exchange)

- Negotiates encryption keys.
- Used with IPsec VPNs.

---

## GRE (Generic Routing Encapsulation)

- Tunneling protocol.
- Encapsulates different network protocols.
- Often combined with IPsec.

---

## RSH (Remote Shell)

- Executes commands on remote Unix systems.
- Sends data without encryption.
- Replaced by SSH.

---

# ⭐ Most Important for HTB Academy

- VPN
- IPsec
- NAT
- STP
- CDP
- TACACS
- EAP / PEAP
- URL
- URI
- AJAX
- CRLF
- IKE
