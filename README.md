[README.md](https://github.com/user-attachments/files/32691331/README.md)
# شبكة IoT معزولة بمبدأ Zero Trust

محاكاة شبكة IoT مقسّمة إلى VLANs معزولة، مبنية على Cisco Packet Tracer،
تطبّق مبدأ Zero Trust عبر ACLs بنظام Default Deny و Port Security.

## نظرة عامة

- 5 VLANs معزولة (كاميرات، حساسات، إدارة، مستخدمين، سيرفرات)
- Router-on-a-Stick مع Sub-interfaces
- DHCP مركزي + DHCP Relay (ip helper-address)
- ACLs بمبدأ Default Deny تتحكم بالتواصل بين كل VLAN
- Port Security (Sticky MAC, Max 1, Violation: Shutdown)

## الأدوات المستخدمة

Cisco Packet Tracer 8.x

## هيكل الشبكة

| VLAN | الاسم | الشبكة | Gateway |
|------|-------|--------|---------|
| 10 | Cameras | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Sensors | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Admin | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Users | 192.168.40.0/24 | 192.168.40.1 |
| 99 | Servers | 192.168.99.0/24 | 192.168.99.1 |

## مصفوفة الصلاحيات (Zero Trust)

- Cameras -> Server فقط
- Sensors -> Server فقط
- Admin -> Cameras + Sensors + Server (ممنوع من Users)
- Users -> Server + إنترنت فقط

## نتائج الاختبار

جميع اختبارات الـ Ping بين VLANs طابقت السلوك المتوقع (مرفقة في ملف التوثيق).

## محتويات المستودع

- `network.pkt` - ملف المشروع الكامل
- `commands/` - كل أوامر CLI (Switch, Router, ACLs, Port Security)
- `docs/documentation.txt` - التوثيق الكامل والجداول
- `screenshots/` - لقطات شاشة للاختبارات (اختياري)

## ملاحظة

Packet Tracer لا يدعم كل مفاهيم Zero Trust الحقيقية (كالتحقق المستمر
لكل جلسة). تم محاكاة المبدأ عبر التجزئة، ACLs، ومصادقة المنافذ ضمن
حدود إمكانيات المحاكي.
