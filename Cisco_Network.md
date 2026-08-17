# Cisco IOS Commands — Quick Revision

A concise reference for common **Cisco IOS commands** used for basic device configuration, interface setup, remote access, verification, and connectivity testing.

---

## 1. Accessing Cisco IOS Modes

```bash
enable
! Move from User EXEC Mode to Privileged EXEC Mode

configure terminal
! Enter Global Configuration Mode

exit
! Move back one level

end
! Return directly to Privileged EXEC Mode
```

### IOS Mode Flow

```text
User EXEC
   │
   └── enable
          ↓
Privileged EXEC
   │
   └── configure terminal
          ↓
Global Configuration
   │
   ├── interface ...
   ├── line console 0
   ├── line vty 0 4
   └── ...
```

---

## 2. Basic Device Configuration

### Set Hostname

```bash
hostname Switch1
! Set the hostname of the switch

hostname Router1
! Set the hostname of the router
```

### Configure Privileged EXEC Password

```bash
enable secret SConf
! Configure an encrypted password for Privileged EXEC Mode
```

> **Note:** Use an appropriate password for each device. `SConf` and `RConf` are examples only.

### Configure MOTD Banner

```bash
banner motd #Authorized access only#
! Display a message when users access the device
```

---

## 3. Console Password

The console line controls local access through the physical console connection.

```bash
line console 0
! Enter Console Line Configuration Mode

password Cisco
! Set the console password

login
! Enable password authentication

exit
! Exit Console Line Configuration Mode
```

### Quick Configuration

```bash
line console 0
password Cisco
login
exit
```

---

## 4. Router Interface Configuration

Configure an IP address and enable a router interface:

```bash
interface gigabitEthernet 0/0
! Enter GigabitEthernet 0/0 Interface Configuration Mode

ip address IP MASK
! Assign an IPv4 address and subnet mask

no shutdown
! Enable the interface

description ...
! Add an optional description

exit
! Exit Interface Configuration Mode
```

### Example

```bash
interface gigabitEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
description LAN Interface
exit
```

### Key Concept

```text
interface
   ↓
Assign IP Address
   ↓
no shutdown
   ↓
Optional Description
```

---

## 5. Switch Management Interface — SVI

An **SVI (Switched Virtual Interface)** can be used as the management interface of a Layer 2 switch.

### Configuration

```bash
interface vlan 1
! Enter VLAN 1 SVI Configuration Mode

ip address 192.168.1.5 255.255.255.0
! Assign a management IP address

no shutdown
! Enable the SVI

exit
! Exit Interface Configuration Mode

ip default-gateway 192.168.1.1
! Configure the default gateway for the switch
```

### Example Network

```text
             PC
              |
        192.168.1.x
              |
           Switch
      Management IP:
        192.168.1.5
              |
           Router
       Default Gateway:
        192.168.1.1
```

### Important Concept

- `192.168.1.5` → **Management IP of the switch**
- `192.168.1.1` → **Default Gateway of the switch**

The switch uses the default gateway when it needs to communicate with a device outside its local subnet.

---

## 6. Example Router Configuration

A router can have multiple interfaces, with each interface belonging to a different network.

```bash
interface gigabitEthernet 0/1
! Configure GigabitEthernet 0/1

ip address 192.168.1.1 255.255.255.0
! Assign an IP address

no shutdown
! Enable the interface

exit
! Exit Interface Configuration Mode

interface gigabitEthernet 0/0
! Configure GigabitEthernet 0/0

ip address 192.168.2.1 255.255.255.0
! Assign an IP address

no shutdown
! Enable the interface

exit
! Exit Interface Configuration Mode
```

### Resulting Network

```text
Network 192.168.1.0/24
        |
       G0/1
   192.168.1.1
      Router
   192.168.2.1
       G0/0
        |
Network 192.168.2.0/24
```

---

## 7. Telnet Configuration

**Telnet** provides remote CLI access through the VTY (Virtual Terminal) lines.

> **Security Note:** Telnet is unencrypted. For real environments, **SSH is preferred**.

### Configuration

```bash
line vty 0 4
! Enter VTY Line Configuration Mode

password Cisco
! Set the VTY password

login
! Enable password authentication

transport input telnet
! Allow Telnet connections

exit
! Exit VTY Configuration Mode
```

### Quick Configuration

```bash
line vty 0 4
password Cisco
login
transport input telnet
exit
```

### Test Telnet from a PC

```bash
telnet 192.168.1.5
! Connect to the switch using Telnet
```

---

## 8. SSH Configuration

**SSH (Secure Shell)** provides encrypted remote CLI access and is preferred over Telnet.

### Step 1 — Configure Hostname

```bash
hostname Router1
! Set the device hostname
```

### Step 2 — Configure Domain Name

```bash
ip domain-name lab.local
! Configure the domain name required for RSA key generation
```

### Step 3 — Create a Local User

```bash
username karim_anany secret cisco
! Create a local user with an encrypted password
```

### Step 4 — Generate RSA Keys

```bash
crypto key generate rsa
! Generate RSA keys used by SSH
```

### Step 5 — Configure VTY Lines

```bash
line vty 0 4
! Enter VTY Line Configuration Mode

login local
! Use the local username database for authentication

transport input ssh
! Allow SSH connections only

exit
! Exit VTY Configuration Mode
```

### Complete SSH Configuration

```bash
hostname Router1
ip domain-name lab.local
username karim_anany secret cisco
crypto key generate rsa

line vty 0 4
login local
transport input ssh
exit
```

### Test SSH from a PC

```bash
ssh -l karim_anany 192.168.1.1
! Connect to the router using SSH with the specified username
```

After authentication:

```bash
enable
! Enter Privileged EXEC Mode
```

> The password requested after `enable` is the password configured with `enable secret`.

---

## 9. Verification Commands

Verification commands are used to inspect the current state and configuration of the device.

### Check Interface Status

```bash
show ip interface brief
! Display interfaces, IP addresses, and their current status
```

> One of the fastest commands for checking interface status.

### Display Detailed Interface Information

```bash
show interfaces
! Display detailed information about interfaces
```

### Display Interface Descriptions

```bash
show interfaces description
! Display interface descriptions and operational status
```

### Display Routing Table

```bash
show ip route
! Display the IPv4 routing table
```

### Display Running Configuration

```bash
show running-config
! Display the current configuration stored in RAM
```

---

## 10. Connectivity Testing

Use `ping` to test network connectivity using **ICMP**.

```bash
ping IP
! Test connectivity to another device
```

### Example

```bash
ping 192.168.1.1
! Test connectivity to the router
```

---

## 11. Save Configuration

Cisco IOS maintains configuration in two important locations:

```text
running-config
    ↓
Current configuration stored in RAM

startup-config
    ↓
Saved configuration stored in NVRAM
```

### Save Running Configuration

```bash
copy running-config startup-config
! Save the current configuration to NVRAM
```

Alternative:

```bash
write
! Save the current configuration
```

> **Important:** If the configuration is not saved to `startup-config`, changes in `running-config` may be lost after a device restart.

---

## 12. PC IP Configuration

On a Windows PC:

```cmd
ipconfig
! Display the PC's IP address, subnet mask, and default gateway
```

For more detailed information:

```cmd
ipconfig /all
! Display detailed network configuration
```

---

# 13. Quick Revision Cheat Sheet

## Interface Configuration

```bash
interface g0/0
ip address IP MASK
no shutdown
description ...
exit
```

**Concept:**

```text
Enter Interface
      ↓
Assign IP Address
      ↓
Enable Interface
      ↓
Add Description (Optional)
      ↓
Exit
```

---

## Switch Management — SVI

```bash
interface vlan 1
ip address 192.168.1.5 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.1.1
```

**Concept:**

```text
Management IP   → 192.168.1.5
Default Gateway → 192.168.1.1
```

---

## Console Access

```bash
line console 0
password Cisco
login
exit
```

**Purpose:** Configure password authentication for console access.

---

## Telnet

```bash
line vty 0 4
password Cisco
login
transport input telnet
exit
```

**Purpose:** Allow remote CLI access using Telnet.

> Telnet is unencrypted. Use SSH whenever possible.

---

## SSH

```bash
hostname Router1
ip domain-name lab.local
username karim_anany secret cisco
crypto key generate rsa

line vty 0 4
login local
transport input ssh
exit
```

**Concept:**

```text
Hostname
   ↓
Domain Name
   ↓
Local User
   ↓
RSA Keys
   ↓
VTY Configuration
   ↓
Local Authentication
   ↓
SSH Access
```

---

## Verification

```bash
show ip interface brief
show interfaces
show interfaces description
show ip route
show running-config
```

**Purpose:** Check interfaces, IP addresses, interface descriptions, routing, and current configuration.

---

## Connectivity

```bash
ping IP
```

**Purpose:** Test network connectivity using ICMP.

---

## Save Configuration

```bash
copy running-config startup-config
```

or:

```bash
write
```

**Purpose:** Save the current configuration so it persists after a restart.
