# 🎾 Chia tiền sân Pickleball

Ứng dụng web HTML + Firebase để quản lý chi phí sân pickleball với đồng bộ hóa realtime. Mọi người chia mã đồng bộ để cùng xem và cập nhật dữ liệu.

## Tính năng

- ✅ Thêm thành viên và chi phí
- ✅ Chia tiền tự động và tính toán tài chính cân bằng
- ✅ Mã đồng bộ 6 ký tự (VD: `A3K9M2`)
- ✅ Đồng bộ realtime qua Firebase
- ✅ Lưu dữ liệu offline (localStorage fallback)
- ✅ Giao diện responsive, đẹp trên mobile

## Cấu trúc dự án

```
pickleball-splitter/
├── index.html           # Frontend HTML/CSS/JS
├── firebase-config.js   # Cấu hình Firebase
├── package.json         # Dependencies
└── README.md           # Hướng dẫn này
```

---

## Hướng dẫn thiết lập

### 1️⃣ Tạo dự án Firebase

#### Bước 1: Đăng nhập Firebase Console
- Truy cập https://console.firebase.google.com
- Đăng nhập với tài khoản Google

#### Bước 2: Tạo project mới
1. Nhấp **"Create Project"**
2. Đặt tên: `pickleball-splitter` (hoặc tên khác tùy ý)
3. Bỏ chọn "Enable Google Analytics" (không cần thiết)
4. Nhấp **Create project**
5. Đợi 30-60 giây cho project khởi tạo

#### Bước 3: Bật Realtime Database
1. Vào menu **Build** → **Realtime Database**
2. Nhấp **Create Database**
3. Chọn vị trí gần nhất (VD: `asia-southeast1` cho Đông Nam Á)
4. Chọn **Start in test mode** (sau này có thể thay đổi rules)
5. Nhấp **Enable**

#### Bước 4: Lấy cấu hình Firebase
1. Vào **Project Settings** (bánh răng ⚙ góc trên trái)
2. Vào tab **General**
3. Scroll xuống tìm mục **Your apps**
4. Nhấp **Add app** → **Web**
5. Đặt tên app: `pickleball-splitter`
6. Copy toàn bộ config JSON

#### Bước 5: Cập nhật firebase-config.js
Mở file `firebase-config.js` và thay thế các giá trị YOUR_* bằng config từ bước trên

---

### 2️⃣ Cấu hình Firebase Security Rules (bảo mật)

1. Vào **Realtime Database** → **Rules**
2. Thay thế toàn bộ rules bằng:

```json
{
  "rules": {
    "rooms": {
      "$roomCode": {
        ".read": true,
        ".write": true,
        ".indexOn": ["syncCode"]
      }
    }
  }
}
```

3. Nhấp **Publish** để áp dụng

---

### 3️⃣ Chạy ứng dụng locally

#### Cách 1: Dùng Python
```bash
cd pickleball-splitter
python -m http.server 8000
```
Truy cập: http://localhost:8000

#### Cách 2: Dùng Node.js
```bash
npm install -g http-server
http-server -p 8000
```

#### Cách 3: Dùng VS Code Live Server
1. Cài extension "Live Server"
2. Right-click `index.html` → "Open with Live Server"

---

### 4️⃣ Deploy lên GitHub

1. Tạo repo mới trên GitHub: https://github.com/new
2. Tên: `pickleball-splitter`
3. Public
4. Nhấp **Create repository**

```bash
git clone https://github.com/YOUR_USERNAME/pickleball-splitter.git
cd pickleball-splitter

# Copy các file vào folder này
# index.html, firebase-config.js, package.json, README.md

git add .
git commit -m "Initial commit: pickleball splitter app"
git branch -M main
git push -u origin main
```

---

### 5️⃣ Deploy lên web miễn phí

#### A. Firebase Hosting (khuyến nghị)
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy --only hosting
```

#### B. GitHub Pages
Vào Settings → Pages → Source: main → Save

#### C. Vercel
Truy cập https://vercel.com/import → chọn repo GitHub → Import

---

## Hướng dẫn sử dụng

### Người tổ chức
1. Thêm tên thành viên
2. Ghi chi phí
3. Sao chép mã đồng bộ
4. Chia mã cho mọi người
5. Xem tài chính cân bằng

### Người tham gia
1. Nhận mã đồng bộ
2. Nhấp "Nhập mã đồng bộ"
3. Dán mã → Đồng bộ
4. Xem dữ liệu realtime

---

## Troubleshooting

❌ **"Đang kết nối Firebase..."**
- Kiểm tra firebase-config.js có giá trị đúng
- Kiểm tra có internet
- Kiểm tra console F12 có lỗi

❌ **Dữ liệu không lưu**
- Enable Realtime Database?
- Rules cho phép đọc/ghi?
- databaseURL đúng?

❌ **Đồng bộ không được**
- Mã phải giống hệt
- Cần internet
- Thử F5 reload

---

## Bảo mật

⚠️ **Chú ý:**
- Mã đồng bộ là công khai
- Nếu ai biết mã thì có thể sửa dữ liệu
- Để bảo mật hơn, thêm password hoặc authentication

---

## Giấy phép

MIT License

---

**Happy splitting! 🎾💰**
