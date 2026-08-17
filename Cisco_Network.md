# Cisco IOS Commands — Quick Revision

## 1. الدخول إلى أوضاع الجهاز

enable
! الانتقال من User EXEC إلى Privileged EXEC

configure terminal
! الدخول إلى Global Configuration Mode

exit
! الرجوع خطوة للخلف

end
! الرجوع مباشرة إلى Privileged EXEC

---

## 2. Basic Device Configuration

hostname Switch1
! تغيير اسم الـSwitch

hostname Router1
! تغيير اسم الـRouter

enable secret SConf
! وضع Password مشفر للـPrivileged EXEC على الـSwitch

enable secret RConf
! وضع Password مشفر للـPrivileged EXEC على الـRouter

banner motd #Authorized access only#
! إنشاء رسالة تظهر عند الدخول إلى الجهاز

«ملاحظة: في التطبيق الفعلي تختار Password واحد مناسب لكل جهاز، ولا تضع "SConf" و"RConf" معًا على نفس الجهاز إلا لو كان ذلك مقصودًا.»

---

## 3. Console Password

line console 0
! الدخول إلى إعدادات الـConsole

password Cisco
! وضع Password للـConsole

login
! تفعيل طلب الـPassword عند الدخول من الـConsole

exit
! الخروج من إعدادات الـConsole

---

## 4. Router Interface Configuration

interface gigabitEthernet 0/0
! الدخول إلى Interface GigabitEthernet 0/0

ip address IP MASK
! وضع IP Address وSubnet Mask

no shutdown
! تشغيل الـInterface

description ...
! إضافة وصف للـInterface

exit
! الخروج من إعدادات الـInterface

مثال:

interface gigabitEthernet 0/0
ip address 192.168.2.1 255.255.255.0
no shutdown
description LAN Interface
exit

---

## 5. Switch Management Interface — SVI

interface vlan 1
! الدخول إلى VLAN 1 لاستخدامها كـManagement Interface

ip address 192.168.1.5 255.255.255.0
! وضع Management IP للسويتش

no shutdown
! تشغيل الـSVI

exit
! الخروج من إعدادات الـInterface

ip default-gateway 192.168.1.1
! تحديد الـDefault Gateway للسويتش

الفكرة:

PC
 |
 | 192.168.1.x
 |
Switch
 | 192.168.1.5
 |
Router
 | 192.168.1.1

الـ"192.168.1.5" هو IP إدارة السويتش، والـ"192.168.1.1" هو Default Gateway للسويتش.

---

## 6. مثال Router Configuration

interface gigabitEthernet 0/1
! الدخول إلى Gig0/1

ip address 192.168.1.1 255.255.255.0
! وضع IP Address وSubnet Mask

no shutdown
! تشغيل الـInterface

exit
! الخروج

interface gigabitEthernet 0/0
! الدخول إلى Gig0/0

ip address 192.168.2.1 255.255.255.0
! وضع IP Address وSubnet Mask

no shutdown
! تشغيل الـInterface

exit
! الخروج

---

## 7. Telnet Configuration

line vty 0 4
! الدخول إلى خطوط VTY الخاصة بالـRemote Access

password Cisco
! وضع Password للـTelnet

login
! جعل الـVTY تطلب الـPassword

transport input telnet
! السماح باتصالات Telnet

exit
! الخروج من إعدادات VTY

اختبار Telnet من الـPC:

telnet 192.168.1.5
! الاتصال بالسويتش عبر Telnet

---

## 8. SSH Configuration

hostname Router1
! تحديد اسم الجهاز، ويجب أن يكون موجودًا قبل إنشاء RSA Keys

ip domain-name lab.local
! تحديد Domain Name المستخدم مع SSH وRSA

username karim_anany secret cisco
! إنشاء Local User مع Password مشفر

crypto key generate rsa
! إنشاء RSA Keys التي يستخدمها SSH

بعد ذلك:

line vty 0 4
! الدخول إلى خطوط VTY

login local
! استخدام Local User Database للمصادقة

transport input ssh
! السماح باتصالات SSH فقط

exit
! الخروج

اختبار SSH من الـPC:

ssh -l karim_anany 192.168.1.1
! الاتصال بالـRouter عبر SSH باستخدام Username محدد

بعد الدخول:

enable
! الانتقال إلى Privileged EXEC

! Password هنا هو Password الـenable secret

---

## 9. Verification Commands

show ip interface brief
! أسرع أمر لفحص الـInterfaces والـIP Address وحالتها

show interfaces
! عرض تفاصيل كاملة عن الـInterfaces

show interfaces description
! عرض الـInterfaces والـDescriptions وحالتها

show ip route
! عرض Routing Table

show running-config
! عرض الـConfiguration الحالية الموجودة في RAM

---

## 10. Connectivity Testing

ping IP
! اختبار الاتصال بجهاز آخر باستخدام ICMP

مثال:

ping 192.168.1.1
! اختبار الاتصال بالـRouter

---

## 11. Save Configuration

copy running-config startup-config
! حفظ الـConfiguration الحالية حتى لا تضيع بعد Restart

مهم جدًا:

running-config
= Configuration الحالية في RAM

startup-config
= Configuration المحفوظة في NVRAM

---

## 12. PC IP Configuration

على Windows PC:

ipconfig
! عرض IP Address وSubnet Mask وDefault Gateway على الـPC

---

## 13. أهم أوامر المراجعة السريعة

Interface

interface g0/0
ip address IP MASK
no shutdown
description ...
exit

الفكرة: تدخل على الـInterface → تضع IP → تشغله → تضيف Description اختياريًا.

---

Switch Management

interface vlan 1
ip address 192.168.1.5 255.255.255.0
no shutdown
exit
ip default-gateway 192.168.1.1

الفكرة: تعطي السويتش Management IP وتحدد الـGateway.

---

Console

line console 0
password Cisco
login
exit

الفكرة: Password للدخول من Console.

---

Telnet

line vty 0 4
password Cisco
login
transport input telnet
exit

الفكرة: السماح بالدخول Remote باستخدام Telnet.

---

SSH

hostname Router1
ip domain-name lab.local
username karim_anany secret cisco
crypto key generate rsa

line vty 0 4
login local
transport input ssh
exit

الفكرة: إنشاء User + RSA Keys ثم جعل الـVTY تستخدم Local Authentication والسماح بـSSH.

---

Verification

show ip interface brief
show interfaces
show interfaces description
show ip route
show running-config

الفكرة: فحص الـInterfaces والـIP والـRouting والـConfiguration.

---

Testing

ping IP

الفكرة: اختبار الـConnectivity.

---

Save
write او
copy running-config startup-config

الفكرة: حفظ الإعدادات بعد الانتهاء
