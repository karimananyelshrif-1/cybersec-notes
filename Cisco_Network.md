# Cisco IOS Commands — Quick Revision

## 1. Device Modes

```bash
enable
! Go from User EXEC to Privileged EXEC

configure terminal
! Enter Global Configuration Mode

exit
! Go back one step

end
! Go directly to Privileged EXEC
```

---

## 2. Basic Device Configuration

```bash
hostname Switch1
! Set the Switch hostname

hostname Router1
! Set the Router hostname

enable secret SConf
! Set an encrypted password for Privileged EXEC on the Switch

enable secret RConf
! Set an encrypted password for Privileged EXEC on the Router

banner motd #Authorized access only#
! Show a message when accessing the device
```

**Note:** Use one suitable password for each device. Do not use `SConf` and `RConf` on the same device unless needed.

---

## 3. Console Password

```bash
line console 0
! Enter Console settings

password Cisco
! Set the Console password

login
! Enable password login

exit
! Exit Console settings
```

---

## 4. Router Interface Configuration

```bash
interface gigabitEthernet 0/0
! Enter GigabitEthernet 0/0

ip address IP MASK
! Set IP Address and Subnet Mask

no shutdown
! Turn on the Interface

description ...
! Add a description

exit
! Exit Interface settings
```

### Example

```bash
interface gigabitEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
description LAN Interface
exit
```

---

## 5. Switch Management Interface — SVI

```bash
interface vlan 1
! Enter VLAN 1 for Management

ip address 192.168.1.5 255.255.255.0
! Set the Management IP

no shutdown
! Turn on the SVI

exit
! Exit Interface settings

ip default-gateway 192.168.1.1
! Set the Switch Default Gateway
```

### Idea

```text
PC
 |
 | 192.168.1.x
 |
Switch
 | 192.168.1.5
 |
Router
 | 192.168.1.1
```

`192.168.1.5` = Switch Management IP

`192.168.1.1` = Switch Default Gateway

---

## 6. Router Configuration Example

```bash
interface gigabitEthernet 0/1
! Enter Gig0/1

ip address 192.168.1.1 255.255.255.0
! Set IP Address and Subnet Mask

no shutdown
! Turn on the Interface

exit
! Exit

interface gigabitEthernet 0/0
! Enter Gig0/0

ip address 192.168.2.1 255.255.255.0
! Set IP Address and Subnet Mask

no shutdown
! Turn on the Interface

exit
! Exit
```

---

## 7. Telnet Configuration

```bash
line vty 0 4
! Enter VTY lines for Remote Access

password Cisco
! Set the Telnet password

login
! Enable password login

transport input telnet
! Allow Telnet connections

exit
! Exit VTY settings
```

### Test Telnet from PC

```bash
telnet 192.168.1.5
! Connect to the Switch using Telnet
```

---

## 8. SSH Configuration

```bash
hostname Router1
! Set the hostname before creating RSA Keys

ip domain-name lab.local
! Set the Domain Name for SSH and RSA

username karim_anany secret cisco
! Create a Local User with an encrypted password

crypto key generate rsa
! Generate RSA Keys for SSH
```

### Then

```bash
line vty 0 4
! Enter VTY lines

login local
! Use the Local User Database

transport input ssh
! Allow SSH connections only

exit
! Exit VTY settings
```

### Test SSH from PC

```bash
ssh -l karim_anany 192.168.1.1
! Connect to the Router using the username
```

### After Login

```bash
enable
! Go to Privileged EXEC

! The password is the enable secret password
```

---

## 9. Verification Commands

```bash
show ip interface brief
! Quickly check Interfaces, IPs, and their status

show interfaces
! Show detailed Interface information

show interfaces description
! Show Interfaces, descriptions, and status

show ip route
! Show the Routing Table

show running-config
! Show the current Configuration in RAM
```

---

## 10. Connectivity Testing

```bash
ping IP
! Test connectivity using ICMP
```

### Example

```bash
ping 192.168.1.1
! Test connectivity to the Router
```

---

## 11. Save Configuration

```bash
copy running-config startup-config
! Save the current Configuration
```

### Important

```text
running-config
= Current Configuration in RAM

startup-config
= Saved Configuration in NVRAM
```

---

## 12. PC IP Configuration

### Windows PC

```bash
ipconfig
! Show IP Address, Subnet Mask, and Default Gateway
```

---

## 13. Quick Review

### Interface

```bash
interface g0/0
ip address IP MASK
no shutdown
description ...
exit
```

**Idea:** Enter Interface → Set IP → Turn it on → Add Description.

---

### Switch Management

```bash
interface vlan 1
ip address 192.168.1.5 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.1.1
```

**Idea:** Set the Switch Management IP and Gateway.

---

### Console

```bash
line console 0
password Cisco
login
exit
```

**Idea:** Set a password for Console access.

---

### Telnet

```bash
line vty 0 4
password Cisco
login
transport input telnet
exit
```

**Idea:** Allow Remote Access using Telnet.

---

### SSH

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

**Idea:** Create User + RSA Keys → Use Local Authentication → Allow SSH.

---

### Verification

```bash
show ip interface brief
show interfaces
show interfaces description
show ip route
show running-config
```

**Idea:** Check Interfaces, IPs, Routing, and Configuration.

---

### Testing

```bash
ping IP
```

**Idea:** Test Connectivity.

---

### Save

```bash
write
```

or

```bash
copy running-config startup-config
```

**Idea:** Save the Configuration.



## 2. إنشاء الـ VLANs على SW1
 
```
enable
configure terminal
vlan 10
 name VLAN10
exit
vlan 20
 name VLAN20
exit
vlan 30
 name VLAN30
exit
```
على **SW**:
```
interface range FastEthernet0/1-2
 switchport mode access
 switchport access vlan 10
exit
 

interface FastEthernet0/3
 switchport mode access
 switchport access vlan 30
exit
 
interface FastEthernet0/4
 switchport mode access
 switchport access vlan 30
exit
```
على **SW2**:
```
vlan 10
vlan 20
vlan 30
exit
 
interface FastEthernet0/1
 switchport mode access
 switchport access vlan 20
exit
 
interface FastEthernet0/2
 switchport mode access
 switchport access vlan 10
exit
 
interface FastEthernet0/3
 switchport mode access
 switchport access vlan 10
exit
```
 
---
 
## 5. عمل الـ Trunk بين SW1 و SW2 (عشان الـ VLANs تعدي بين السويتشين)
 
على **SW1**:
```
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit
```
على **SW2** (نفس الشيء على البورت المتوصل بـ SW1):
```
interface GigabitEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit
```
## 7. الإعداد جوه الراوتر (Router-on-a-Stick)
 
```
enable
configure terminal
 
interface GigabitEthernet0/0
 no shutdown
exit
 
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 10.0.0.62 255.255.255.192
exit
 
interface GigabitEthernet0/0.20
 encapsulation dot1Q 20
 ip address 10.0.0.126 255.255.255.192
exit
 
interface GigabitEthernet0/0.30
 encapsulation dot1Q 30
 ip address 10.0.0.190 255.255.255.192
exit
```
## 6. عمل الترانك بين SW2 والراوتر (أو الـ Multilayer Switch)
 
على **SW2**، البورت المتوصل بالراوتر لازم يبقى Trunk برضه عشان ينقل الـ 3 VLANs في كابل واحد:
```
interface FastEthernet0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit
```
## 8. البديل: الإعداد جوه الـ Multilayer Switch بدل الراوتر
 
لو حذفنا الراوتر وحطينا مكانه Multilayer Switch:
 
```
enable
configure terminal
 
ip routing
 
vlan 10
vlan 20
vlan 30
exit
 
interface FastEthernet0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
exit
 
interface vlan 10
 ip address 10.0.0.62 255.255.255.192
 no shutdown
exit
 
interface vlan 20
 ip address 10.0.0.126 255.255.255.192
 no shutdown
exit
 
interface vlan 30
 ip address 10.0.0.190 255.255.255.192
 no shutdown
exit
```
