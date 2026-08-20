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
# OSPF & ACL — Practical Command Templates

كل قسم هنا عبارة عن **سيناريو كامل** (Template) — مش أوامر متفرقة. تاخد البلوك كله وتطبقه، وتحته شرح مختصر لكل سطر جوه نفس السياق.

---

## 1. OSPF — التشغيل الأساسي (Basic Setup)

```cisco
enable
configure terminal

interface loopback 0
 ip address 1.1.1.1 255.255.255.255
exit

router ospf 10
 router-id 1.1.1.1
 network 10.1.1.0 0.0.0.255 area 0
 network 10.1.2.0 0.0.0.255 area 0
 passive-interface loopback 0
exit

end
```

**السياق:** ده الـ Template اللي بتبدأ بيه أي راوتر جديد على OSPF.
- `interface loopback 0` + `ip address` → بتعمل هوية ثابتة للراوتر (مش بتقع زي الـ physical interfaces).
- `router ospf 10` → بتفتح عملية OSPF برقم Process ID اختياري (محلي على الراوتر بس).
- `router-id 1.1.1.1` → بتربط الـ OSPF بالـ Loopback عشان الراوتر يتعرف بنفس الهوية دايمًا.
- `network ... area 0` → بتحدد أي Interfaces (بناءً على الـ IP) هتشارك في OSPF Area 0.
- `passive-interface loopback 0` → بما إن الـ Loopback مش متوصل بحد، بتمنعه يبعت Hello عبط.

**تحقق:**
```cisco
show ip protocols
show ip ospf neighbor
show ip route
```

---

## 2. OSPF — الإعداد على الـ Interface مباشرة (بديل لـ network command)

```cisco
interface GigabitEthernet0/0/0
 ip ospf 10 area 0
exit
```

**السياق:** بديل لأمر `network` — بدل ما تحدد الشبكة وتسيب الراوتر يدور على الـ interface المطابقة، بتحط OSPF على الـ interface نفسه مباشرة بنفس الـ Process ID والـ Area. الطريقتين بيوصلوا لنفس النتيجة.

---

## 3. OSPF — التحكم في الأداء والانتخابات (DR/BDR + Cost + Timers)

```cisco
interface GigabitEthernet0/0/0
 ip ospf priority 255
 ip ospf cost 10
 ip ospf hello-interval 5
 ip ospf dead-interval 20
exit

router ospf 10
 auto-cost reference-bandwidth 1000
exit
```

**السياق:** البلوك ده بتستخدمه لما تحب تتحكم في **سلوك OSPF** مش بس تشغّله.
- `priority 255` → بتخلي الـ interface ده مرشّح أقوى يبقى DR في انتخابات DR/BDR (لو priority = 0 مبيترشحش خالص).
- `cost 10` → بتفرض Cost يدوي بدل ما OSPF يحسبه لوحده (أقل Cost = مسار أفضل).
- `hello-interval` / `dead-interval` → بتتحكم في سرعة اكتشاف إن الجار وقع (لازم يبقوا **متطابقين** على الطرفين وإلا الـ Neighbor مش هيبني).
- `auto-cost reference-bandwidth 1000` → بتغيّر القيمة اللي عليها بيتحسب الـ Cost (Formula: `Cost = Reference BW ÷ Interface BW`)، ولازم تتظبط بنفس القيمة على كل راوترات الشبكة.

**تحقق:**
```cisco
show ip ospf interface
show ip ospf neighbor
```

---

## 4. OSPF — إزالة/إعادة ضبط (Rollback)

```cisco
router ospf 10
 no network 10.1.1.0 0.0.0.255 area 0
exit

interface GigabitEthernet0/0/0
 no ip ospf hello-interval
 no ip ospf dead-interval
exit

clear ip ospf process
```

**السياق:** البلوك ده بتستخدمه لما تلاقي إعداد غلط وعايز ترجع للـ Default أو تشيل statement بعينه، وبعدين تعمل `clear ip ospf process` عشان يعيد الانتخابات والـ Neighbors من الأول.

---

## 5. Standard ACL — Deny Host واحد واسمح للباقي

```cisco
enable
configure terminal

access-list 1 deny host 192.168.10.10
access-list 1 permit any

interface GigabitEthernet0/0/0
 ip access-group 1 in
exit

end
```

**السياق:** ده أبسط Template لـ ACL — **امنع جهاز واحد، واسمح لكل حاجة تانية.**
- السطرين الأول بيبنوا نفس الـ ACL رقم 1 (كل سطر يضيف ACE جديد بالترتيب).
- لازم `permit any` في الآخر، وإلا أي حد غير الـ 192.168.10.10 هيتمنع بسبب الـ **Implicit Deny** المخفي في نهاية كل ACL.
- `ip access-group 1 in` هي اللي فعليًا بتفعّل الـ ACL على الـ interface — من غيرها الـ ACL بيفضل موجود بس مش شغال.

**تحقق:**
```cisco
show access-lists
show ip interface
```

---

## 6. Named Standard ACL — نفس الفكرة بس بالاسم

```cisco
enable
configure terminal

ip access-list standard NO-ACCESS
 deny host 192.168.10.10
 permit any
exit

interface GigabitEthernet0/0/0
 ip access-group NO-ACCESS in
exit

end
```

**السياق:** نفس منطق البلوك اللي فات بالظبط، الفرق الوحيد إن الـ ACL بقى ليه **اسم واضح** (`NO-ACCESS`) بدل رقم، وده بيسهّل قراءة الكونفيج لما يكبر عندك عدد الـ ACLs.

---

## 7. Extended ACL — السماح بـ HTTP/HTTPS بس من شبكة معينة

```cisco
enable
configure terminal

ip access-list extended SURFING
 permit tcp 192.168.10.0 0.0.0.255 any eq 80
 permit tcp 192.168.10.0 0.0.0.255 any eq 443
exit

interface GigabitEthernet0/0/0
 ip access-group SURFING in
exit

end
```

**السياق:** Template كامل لفلترة أدق — بيسمح بس بحركة TCP على بورتات 80 و443 (HTTP/HTTPS) من شبكة `192.168.10.0/24`، وأي حركة تانية بتتمنع تلقائيًا بسبب الـ Implicit Deny (مفيش `permit any` هنا، فده Firewall ضيق مقصود).
- الـ Extended هنا بيتحط قريب من الـ **Source** (المفروض يكون على الراوتر الأقرب لشبكة 192.168.10.0)، عكس الـ Standard اللي بيتحط قريب من الـ Destination.

**تحقق:**
```cisco
show access-lists
show running-config
```

---

## 8. تعديل ACE موجود من غير ما تمسح الـ ACL كله

```cisco
ip access-list extended SURFING
 no 10
 10 permit tcp 192.168.10.0 0.0.0.255 any eq 80
exit
```

**السياق:** لما تلاقي ACE معينة (برقم Sequence زي 10) غلط، بتمسحها بس (`no 10`) وتضيف مكانها الصح بنفس الرقم — من غير ما تلمس باقي الـ ACL.

---

## مرجع سريع للـ Keywords والـ Wildcard

| Keyword | المعنى | Wildcard المعادل |
|---|---|---|
| `host` | IP واحد بالظبط | `0.0.0.0` |
| `any` | أي IP | `255.255.255.255` |
| `eq 80` / `eq 443` | HTTP / HTTPS | — |
| `established` | حركة رد على Session TCP قائمة أصلًا | — |

`Wildcard = 255.255.255.255 − Subnet Mask` → (`0` = Match, `1` = Ignore)

---

## قواعد ذهبية (تفتكرها في أي سيناريو)

```text
OSPF: أقل Cost = أفضل مسار
ACL:  أول Match بيتنفذ، والباقي كله بيقع في Implicit Deny لو مفيش permit any
كل Interface: ACL واحد بس IN + ACL واحد بس OUT
Extended ACL → قريب من الـ Source
Standard ACL → قريب من الـ Destination
```

---

## Troubleshooting — بلوك واحد لكل مشكلة

**OSPF Neighbor مش بيتكون:**
```cisco
show ip ospf neighbor
show ip ospf interface
show ip protocols
```
راجع: Subnet mask – Hello/Dead interval متطابقين ولا لأ – Area – الـ IP بيقع جوه range الـ network statement.

**ACL مش بيفلتر زي المتوقع:**
```cisco
show access-lists
show running-config
show ip interface
```
راجع: الـ ACL متطبق على الـ interface الصح – الاتجاه (in/out) صح – مفيش ACE قبلها بتاخد الحركة بالغلط – الحركة مش واقعة في implicit deny من غير ما تقصد.


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
