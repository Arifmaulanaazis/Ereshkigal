<h1 align="center">Ereshkigal</h1>

<p align="center">
  <img src="icon.png" alt="Ereshkigal Icon" width="300" height="300" style="object-fit: cover;">
</p>

<p align="center">
  <a href="https://hits.seeyoufarm.com"><img src="https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https%3A%2F%2Fgithub.com%2FArifmaulanaazis%2FEreshkigal&count_bg=%2379C83D&title_bg=%23555555&icon=&icon_color=%23E7E7E7&title=Total+Viewer&edge_flat=false"/></a>
  <img src="https://img.shields.io/github/downloads/Arifmaulanaazis/Ereshkigal/total?style=flat-square" alt="GitHub downloads"/>
</p>

<h2 align="center">Lisensi</h2>
<p align="center"><strong>Lisensi:</strong> GPLv3</p>

## Pilih Bahasa / Select Language / Chọn Ngôn Ngữ / เลือกภาษา / 言語を選択
- [Indonesia](README.md)
- [English](README-English.md)
- [Vietnamese](README-Vietnam.md)
- [Thailand](README-Thailand.md)
- [Japanese](README-Japanese.md)


## รายละเอียดแอปพลิเคชัน
Ereshkigal เป็นแอปพลิเคชันการทดสอบการฉีดแพ็คเกจ (deauther) WiFi ที่ออกแบบมาให้ใช้กับโมดูล RTL8720DN แอปพลิเคชันนี้ช่วยให้ผู้ใช้ทดสอบเครือข่าย WiFi โดยการโจมตี deauthentication และระบุจุดเข้าถึงที่อ่อนแอ

## ฟีเจอร์ของแอปพลิเคชัน
- การฉีดแพ็คเกจ deauthentication เพื่อทดสอบความปลอดภัยของเครือข่าย WiFi
- อินเทอร์เฟซผู้ใช้ที่เรียบง่ายและใช้งานง่าย
- รองรับโมดูล RTL8720DN (AI-Thinker BW16)
- รองรับการฉีดแพ็คเกจ deauthentication ในเครือข่าย 2.4GHz และ 5GHz
- กระบวนการแฟลชที่ง่ายด้วย Ereshkigal Flasher

## อุปกรณ์ที่ต้องใช้
- โมดูล RTL8720DN (AI-Thinker BW16) [ซื้อที่นี่](https://tokopedia.link/

1k7qXB2VENb)
- สาย USB Type C สำหรับเชื่อมต่อระหว่างโมดูลและคอมพิวเตอร์
- คอมพิวเตอร์ที่ใช้ระบบปฏิบัติการ Windows
- Ereshkigal V1.0.3.bin (ไฟล์ไบนารีของแอปพลิเคชัน)
- Ereshkigal Flasher V1.0.0.exe (แอปพลิเคชันสำหรับแฟลช)

## วิดีโอแนะนำการติดตั้งและการใช้งาน
สำหรับแนะนำการติดตั้งและการใช้งานโปรดชมวิดีโอที่ [YouTube](https://youtu.be/r1fH1nWJnAg)

## วิธีการแฟลช
1. เชื่อมต่อโมดูล RTL8720DN เข้ากับคอมพิวเตอร์ด้วยสาย USB Type C
2. ดาวน์โหลดและเปิด Ereshkigal Flasher V1.0.0.exe
3. เลือกไฟล์ Ereshkigal V1.0.3.bin ที่คุณดาวน์โหลดมา
4. คลิกปุ่ม "Start Flash" เพื่อเริ่มกระบวนการแฟลช
5. รอจนกระทั่งกระบวนการแฟลชเสร็จสมบูรณ์ โมดูลจะรีบูตโดยอัตโนมัติ

## วิธีการใช้งาน
1. หลังจากแฟลชเสร็จแล้ว เชื่อมต่อโมดูลกับแหล่งจ่ายไฟ
2. เปิดเครือข่าย WiFi ของคุณและคุณจะพบ SSID ชื่อ Ereshkigal
3. รหัสผ่าน Ereshkigal คือ masukangin
4. เมื่อเชื่อมต่อกับ Ereshkigal แล้ว ให้เปิดที่อยู่ IP 192.168.1.1
5. เลือกเครือข่าย WiFi ที่คุณต้องการทดสอบด้วยการเลือกเครือข่าย
6. กดปุ่ม "Deauth" เพื่อเริ่มการทดสอบ
7. ใช้ปุ่ม "Scan" เพื่อสแกนเครือข่ายใหม่
8. ใช้ปุ่ม "RST" บน RTL8720DN เพื่อหยุดการทดสอบ

---

**หมายเหตุ:** กรุณาใช้แอปพลิเคชันนี้เฉพาะสำหรับการทดสอบเครือข่ายส่วนตัวและตามกฎหมายที่บังคับใช้
