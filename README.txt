1) แตกไฟล์/เปิดโปรเจกต์
- แตกไฟล์ ZIP แล้วควรมีโฟลเดอร์หลัก: client/ และ server/

2) สร้างฐานข้อมูล MySQL
- เข้า MySQL แล้วสร้าง DB (ชื่อให้ตรงกับ DATABASE_URL)
  ตัวอย่าง:
  CREATE DATABASE ai_ecom CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

3) ติดตั้งและรันฝั่ง Server (Node + Prisma)
3.1 ติดตั้งแพ็กเกจ
- cd server
- npm install
- npm i nodemon

3.2 ตั้งค่าไฟล์ server/.env (ใส่ค่าของคุณเอง)
- DATABASE_URL="mysql://USER:PASS@localhost:3306/DBNAME"
- SECRET="your_secret"
- STRIPE_SECRET_KEY="sk_test_xxx"
- CLOUDINARY_CLOUD_NAME="xxx"
- CLOUDINARY_API_KEY="xxx"
- CLOUDINARY_API_SECRET="xxx"
(ถ้าโปรเจกต์ใช้ส่งอีเมล)
- EMAIL_USER="xxx"
- EMAIL_PASS="xxx"   (แนะนำเป็น Gmail App Password)

หมายเหตุสำคัญ:
- ถ้าเคยแชร์ .env ที่มี key จริง ให้เปลี่ยน/rotate key ทันที และอย่า commit .env

3.3 สร้างตาราง + Generate Prisma Client
- npx prisma migrate dev
- npx prisma generate

3.4 รัน Server
- npm start
- เปิดทดสอบ: http://localhost:5001 (พอร์ตอาจต่างตามโปรเจกต์)

4) ติดตั้งและรันฝั่ง Client (React/Vite)
4.1 ติดตั้งแพ็กเกจ
- cd client
- npm install

4.2 (ถ้าใช้ Stripe ฝั่งหน้าเว็บ) สร้าง client/.env
- VITE_STRIPE_PK="pk_test_xxx"

4.3 รัน Client
- npm run dev
- เข้าเว็บ: http://localhost:5173

5) ทำให้เป็น Admin (ถ้าต้องการ)
- cd server
- npx prisma studio
- แก้ user ที่ต้องการให้ role = "admin"

6) ปัญหาที่พบบ่อย (สั้นๆ)
- @prisma/client did not initialize yet:
  cd server && npx prisma generate
- ต่อ DB ไม่ได้:
  เช็ค DATABASE_URL, MySQL เปิดอยู่, และสร้าง DB แล้ว
- Client ยิง API ไม่ได้:
  เช็ค server รันอยู่, URL API ใน client/src/api/* และพอร์ตให้ตรงกัน
