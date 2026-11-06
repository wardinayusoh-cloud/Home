# ระบบชำระค่าบ้าน (Supabase)

## ไฟล์
- `index.html` หน้านักเรียน (กรอกชื่อ + รหัส → เห็นยอดค้าง → ชำระเงิน)
- `admin.html` หลังบ้าน (สรุปรายคน, ตรวจสลิป, แจ้งเตือน, จัดการนักเรียน)
- `schema.sql` สร้างตารางทั้งหมดใน Supabase
- `qr.png` รูป QR รับเงินของคุณ (ต้องใส่เอง วางโฟลเดอร์เดียวกับ index.html)

## ขั้นตอนติดตั้ง
1. สร้างโปรเจกต์ที่ supabase.com
2. SQL Editor → วางเนื้อหา `schema.sql` → Run
3. Authentication → Users → Add user (อีเมล + รหัสผ่านของแอดมิน) แล้วคัดลอก UUID
4. SQL Editor รัน: `insert into admins (user_id) values ('UUID ที่คัดลอก');`
5. Authentication → Providers → Email → **ปิด "Allow new users to sign up"** (กันคนอื่นสมัครเอง)
6. Project Settings → API คัดลอก **Project URL** และ **anon public key** ไปใส่ที่ด้านบนของสคริปต์ใน `index.html` และ `admin.html`
7. อัปโหลดทั้งโฟลเดอร์ขึ้น Netlify / Vercel / GitHub Pages / Cloudflare Pages (ฟรี)
8. เข้า `admin.html` → แท็บ "จัดการนักเรียน" → เพิ่มรายชื่อ + รหัส 4 หลัก + เดือนที่เริ่มนับ

## หมายเหตุ
- ห้ามใส่ service_role key ในไฟล์ HTML เด็ดขาด ใช้เฉพาะ anon key
- นักเรียนไม่สามารถอ่านตารางตรง ๆ ได้ ต้องผ่านฟังก์ชัน (ชื่อ + รหัส) เท่านั้น
- ยอดค้างคำนวณจาก: เดือนที่เริ่มนับ → เดือนปัจจุบัน แล้วหักรายการที่ไม่ใช่ "ไม่ผ่าน"
- แจ้งเตือนจะขึ้นเป็นกล่องเหลืองในหน้านักเรียนครั้งต่อไปที่เข้าระบบ
