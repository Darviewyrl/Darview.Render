
# การอัปเดต

เก็บบันทึกข้อมูลการอัปเดต Project ในแต่ละวัน เพื่อสามารถเข้ามาดูการแก้ไขไฟล์/โค้ดต่างๆได้

## Client

### วันที่ 27 เมษายน 2024

1. ปรับให้ไฟล์ blacklist_IP:PORT.txt เป็นชื่อ blacklist.txt เฉยๆ
2. รับรองภาษาไทย

### วันที่ 26 เมษายน 2024

1. เปลี่ยนชื่อจาก sampvoice เป็น darrender (ยกเว้น sampvoice.sln)
2. ลบ sv ออกจากชื่อไฟล์ svlog, svconfig, svblacklist
3. เอาไฟล์ darrender.inc มาลง
4. ลบ sv: ใน Log ออก
5. อัปเดตเวอร์ชัน client, control, voice, project เป็น 2.01 หรือ MakeVersion(2, 0, 1)
6. ถ้าไม่เข้าเซิร์ฟตัวเอง จะเด้งออกเกมอัตโนมัติ

## Server

### วันที่ 28 เมษายน 2024

1. ปรับให้ไฟล์ blacklist_IP:PORT.txt เป็นชื่อ blacklist.txt เฉยๆ
2. รับรองภาษาไทย
