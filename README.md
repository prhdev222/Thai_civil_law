# 📜 เรียนกฎหมายแพ่งฯ — ป.พ.พ. บรรพ ๑–๒

แพลตฟอร์มเรียนกฎหมายแพ่งและพาณิชย์ (บรรพ ๑ หลักทั่วไป + บรรพ ๒ หนี้)
พร้อม Mind Map, YouTube Database, Lecture Notes — Deploy ไป Vercel

## 🚀 Deploy ไป Vercel (๓ ขั้นตอน)

### ขั้นที่ ๑ — เตรียมโปรเจค

```bash
# แตกไฟล์
tar xzf civil-law-deploy.tar.gz
cd civil-law

# ติดตั้ง
npm install

# ทดสอบ local
npm run dev
# → http://localhost:5173
```

### ขั้นที่ ๒ — Deploy ไป Vercel

```bash
# วิธี A: Vercel CLI (เร็วที่สุด)
npx vercel login
npx vercel --prod

# วิธี B: ผ่าน GitHub
# 1. git init && git add . && git commit -m "init"
# 2. push ไป GitHub
# 3. ไปที่ vercel.com → Import Project → เลือก repo
# 4. Framework: Vite / Build: npm run build / Output: dist
# 5. Deploy!
```

### ขั้นที่ ๓ — เชื่อม Turso (ถ้าต้องการ sync ข้อมูล)

```bash
# สร้าง Turso DB
turso db create civil-law-db
turso db shell civil-law-db < migrations/001_init.sql

# ดู URL + สร้าง Token
turso db show civil-law-db --url
turso db tokens create civil-law-db

# เพิ่ม Environment Variables ใน Vercel Dashboard:
# Settings → Environment Variables
# TURSO_URL = libsql://civil-law-db-xxx.turso.io
# TURSO_AUTH_TOKEN = eyJhbG...
```

## 📂 โครงสร้างไฟล์

```
civil-law/
├── src/
│   ├── App.jsx          # แอปหลัก (~60 มาตรา + 4 tabs)
│   ├── main.jsx         # React entry
│   └── index.css        # Tailwind CSS
├── migrations/
│   └── 001_init.sql     # SQL schema (Turso)
├── public/favicon.svg   # 📜 favicon
├── index.html
├── package.json
├── vite.config.js
├── tailwind.config.js
├── postcss.config.js
├── vercel.json          # Vercel config
└── README.md
```

## 📊 เนื้อหาที่รวมไว้

### บรรพ ๑ หลักทั่วไป (~30 มาตรา)
| ลักษณะ | มาตราสำคัญ |
|--------|-----------|
| ๑ บทเบ็ดเสร็จทั่วไป | ม.๔ (ใช้กฎหมาย), ม.๕–๖ (สุจริต), ม.๗ (ดอกเบี้ย 3%), ม.๘ (เหตุสุดวิสัย), ม.๙ (ลายมือชื่อ) |
| ๒ บุคคล | ม.๑๕ (สภาพบุคคล), ม.๑๙ (บรรลุนิติภาวะ), ม.๒๑ (ผู้เยาว์ทำนิติกรรม), ม.๒๘–๓๒ (ไร้/เสมือนไร้ความสามารถ), ม.๖๑–๖๔ (สาบสูญ), ม.๖๕ (นิติบุคคล) |
| ๓ ทรัพย์ | ม.๑๓๗–๑๔๐ (ทรัพย์/ทรัพย์สิน/อสังหา/สังหา), ม.๑๔๔ (ส่วนควบ), ม.๑๔๗ (อุปกรณ์), ม.๑๔๘ (ดอกผล) |
| ๔ นิติกรรม | ม.๑๔๙ (นิยาม), ม.๑๕๐–๑๕๖ (โมฆะ), ม.๑๕๓–๑๕๙ (โมฆียะ), ม.๑๖๔ (ข่มขู่), ม.๑๗๒–๑๘๑ (โมฆะ/โมฆียะ ผล), ม.๑๘๒–๑๙๓ (เงื่อนไข/เงื่อนเวลา) |
| ๕ ระยะเวลา | ม.๑๙๓/๑–๑๙๓/๘ (การนับระยะเวลา) |
| ๖ อายุความ | ม.๑๙๓/๙–๑๙๓/๑๔ (สะดุดหยุดลง), ม.๑๙๓/๓๐ (อายุความทั่วไป 10 ปี) |

### บรรพ ๒ หนี้ (~30 มาตรา)
| ลักษณะ | มาตราสำคัญ |
|--------|-----------|
| ๑ บทเบ็ดเสร็จทั่วไป | ม.๑๙๔ (อำนาจแห่งมูลหนี้), ม.๒๐๓ (ชำระโดยพลัน), ม.๒๑๓–๒๒๔ (ผิดนัด ค่าเสียหาย ดอกเบี้ย 5%), ม.๒๙๑ (ลูกหนี้ร่วม), ม.๓๔๑ (หักกลบลบหนี้) |
| ๒ สัญญา | ม.๓๕๔–๓๖๑ (คำเสนอ/คำสนอง), ม.๓๖๙ (ต่างตอบแทน), ม.๓๗๗–๓๗๘ (มัดจำ), ม.๓๗๙–๓๘๕ (เบี้ยปรับ), ม.๓๘๖–๓๙๔ (เลิกสัญญา) |
| ๓ จัดการงานนอกสั่ง | ม.๓๙๕–๔๐๑ (Negotiorum Gestio) |
| ๔ ลาภมิควรได้ | ม.๔๐๖ (Unjust Enrichment) |
| ๕ ละเมิด | ม.๔๒๐–๔๒๑ (หลักละเมิด), ม.๔๒๕–๔๓๒ (นายจ้าง ผู้เยาว์ ร่วมทำ), ม.๔๓๘–๔๔๘ (ค่าสินไหม อายุความ), ม.๔๔๙ (นิรโทษกรรม) |

## ⚙️ ตั้งค่า Custom Domain

```bash
# ใน Vercel Dashboard → Settings → Domains
# เพิ่ม: civil.prhmedicine.cloud
# ตั้ง CNAME: civil → cname.vercel-dns.com
```

## 🔒 เพิ่ม PIN Auth (Optional)

เพิ่มที่ต้นไฟล์ App.jsx:
```javascript
const [auth, setAuth] = useState(false);
const [pin, setPin] = useState('');
if (!auth) return (/* PIN form, check pin === '1234' */);
```

## 📋 License

เพื่อการศึกษาเท่านั้น อ้างอิง: ป.พ.พ. แก้ไขถึง พ.ศ.๒๕๖๔ — สำนักงานคณะกรรมการกฤษฎีกา
