# FLIC - Hệ Thống Quản Lý Biểu Mẫu
## Fullstack: Node.js + Express + MongoDB + HTML/CSS/JS

---

## Cấu Trúc Dự Án

```
flic-fullstack/
├── backend/                  ← Server Node.js + Express
│   ├── config/
│   │   └── database.js       ← Kết nối MongoDB
│   ├── middleware/
│   │   └── auth.js           ← Xác thực JWT
│   ├── models/
│   │   ├── User.js           ← Schema người dùng
│   │   ├── Form.js           ← Schema form mẫu
│   │   └── Response.js       ← Schema phản hồi
│   ├── routes/
│   │   ├── auth.js           ← Đăng nhập / Đăng ký
│   │   ├── forms.js          ← CRUD Form
│   │   ├── responses.js      ← Quản lý phản hồi
│   │   ├── users.js          ← Quản lý nhân viên
│   │   └── dashboard.js      ← Thống kê
│   ├── .env.example          ← Mẫu biến môi trường
│   ├── package.json
│   ├── seed.js               ← Tạo dữ liệu mẫu
│   └── server.js             ← File chính
│
└── frontend/                 ← Giao diện HTML/CSS/JS
    ├── css/main.css
    ├── js/
    │   ├── api.js            ← Kết nối API
    │   ├── main.js
    │   ├── layout.js
    │   └── pages/
    ├── pages/
    └── index.html
```

---

## Yêu Cầu Cài Đặt

- **Node.js** >= 18 → https://nodejs.org
- **MongoDB** (chọn 1 trong 2):
  - MongoDB Local: https://www.mongodb.com/try/download/community
  - MongoDB Atlas (Cloud - Miễn phí): https://www.mongodb.com/atlas

---

## Hướng Dẫn Chạy (Step by Step)

### Bước 1 — Cài MongoDB Atlas (Cloud, dễ nhất)

1. Vào https://www.mongodb.com/atlas → Đăng ký miễn phí
2. Tạo cluster → Chọn **Free (M0)**
3. Tạo user database (username/password)
4. Network Access → Add IP → **0.0.0.0/0** (cho phép mọi IP)
5. Connect → Copy connection string:
   ```
   mongodb+srv://username:password@cluster.mongodb.net/flic_db
   ```

### Bước 2 — Cấu Hình Backend

```bash
cd backend

# Sao chép file cấu hình
copy .env.example .env       # Windows
cp .env.example .env         # Mac/Linux

# Mở .env và điền thông tin:
# MONGO_URI=mongodb+srv://username:password@cluster.mongodb.net/flic_db
# JWT_SECRET=flic_secret_key_2026
```

### Bước 3 — Cài Thư Viện

```bash
cd backend
npm install
```

### Bước 4 — Tạo Dữ Liệu Mẫu

```bash
cd backend
node seed.js
```

Kết quả:
```
✅ Kết nối MongoDB thành công
👥 Đã tạo 3 tài khoản
📋 Đã tạo 2 form mẫu
✅ Seed dữ liệu hoàn tất!

Tài khoản mặc định:
  admin   / 123456  (Quản trị viên)
  manager / 123456  (Quản lý)
  staff   / 123456  (Nhân viên)
```

### Bước 5 — Chạy Server

```bash
cd backend
node server.js
```

Mở trình duyệt: **http://localhost:3000**

---

## API Endpoints

| Method | URL | Mô tả | Cần login |
|--------|-----|-------|-----------|
| POST | /api/auth/login | Đăng nhập | ❌ |
| POST | /api/auth/register | Đăng ký | ✅ |
| GET | /api/auth/me | Lấy thông tin | ✅ |
| GET | /api/forms | Danh sách form | ✅ |
| POST | /api/forms | Tạo form mới | ✅ |
| PUT | /api/forms/:id | Cập nhật form | ✅ |
| DELETE | /api/forms/:id | Xóa form | ✅ |
| POST | /api/responses/submit | Gửi form | ❌ |
| GET | /api/responses | Xem phản hồi | ✅ |
| GET | /api/users | Danh sách nhân viên | ✅ |
| POST | /api/users | Thêm nhân viên | ✅ Admin |
| GET | /api/dashboard/stats | Thống kê | ✅ |

---

## Deploy Lên Internet (Tùy Chọn)

### Backend → Railway (Miễn phí)

1. Vào https://railway.app → Đăng ký
2. New Project → Deploy from GitHub
3. Thêm biến môi trường:
   - `MONGO_URI` = connection string MongoDB Atlas
   - `JWT_SECRET` = chuỗi bí mật
   - `PORT` = 3000
4. Lấy URL deploy (vd: `https://flic-api.railway.app`)

### Frontend → Netlify (Miễn phí)

1. Vào https://netlify.com → Đăng ký
2. Kéo thả thư mục `frontend` vào Netlify
3. Mở `frontend/js/api.js`, đổi:
   ```js
   const API_BASE = 'https://flic-api.railway.app/api'; // URL Railway của bạn
   ```
4. Deploy lại

---

## Công Nghệ Sử Dụng

| Phần | Công nghệ |
|------|-----------|
| Frontend | HTML5, CSS3, JavaScript thuần |
| Backend | Node.js + Express.js |
| Database | MongoDB + Mongoose |
| Xác thực | JWT (JSON Web Token) |
| Mã hóa mật khẩu | bcryptjs |
