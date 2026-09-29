<div align="center">

# ☕ CafePOS — Hệ Thống POS Thông Minh cho F&B

**Professional Point-of-Sale System for Cafes, Bubble Tea Shops & F&B Businesses**

[![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)](.)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Node](https://img.shields.io/badge/Node.js-20%2B-339933?style=flat-square&logo=node.js)](https://nodejs.org)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react)](https://react.dev)
[![Electron](https://img.shields.io/badge/Electron-28-47848F?style=flat-square&logo=electron)](https://electronjs.org)
[![SQLite](https://img.shields.io/badge/SQLite-embedded-003B57?style=flat-square&logo=sqlite)](https://sqlite.org)

[Tiếng Việt](#-giới-thiệu) · [English](#-introduction)

</div>

---

## 🇻🇳 Giới Thiệu

**CafePOS** là hệ thống quản lý bán hàng (Point-of-Sale) chuyên nghiệp, được thiết kế riêng cho các quán **cafe, trà sữa, nhà hàng fast food và F&B** tại Việt Nam.

Hệ thống hoạt động theo mô hình **Server + Client** — máy chủ chạy trên Windows tại quán, các thiết bị khác (máy tính, tablet, điện thoại) kết nối qua **mạng LAN nội bộ** hoặc **Cloudflare Tunnel** để truy cập từ xa.

> **Không cần Internet để vận hành** — Toàn bộ dữ liệu lưu cục bộ bằng SQLite. Cloudflare Tunnel chỉ dùng khi muốn truy cập từ xa hoặc nhiều chi nhánh.

---

## 🇬🇧 Introduction

**CafePOS** is a professional Point-of-Sale management system designed specifically for **Vietnamese cafes, bubble tea shops, restaurants, and F&B businesses**.

It follows a **Server + Client** architecture — the server runs on-premise (Windows PC), and all other devices connect via **local LAN** or **Cloudflare Tunnel** for remote access.

> **No Internet required for daily operation** — All data is stored locally via SQLite. Cloudflare Tunnel is optional for remote/multi-branch access.

---

## ✨ Tính Năng Chính / Key Features

| Module | Chức năng / Feature |
|--------|-------------------|
| 🖥️ **POS Bán hàng** | Gọi món nhanh, tùy chỉnh size, topping, đường, đá, ghi chú |
| 🗺️ **Quản lý bàn** | Sơ đồ bàn theo khu vực, trạng thái real-time |
| 👨‍🍳 **KDS Bếp** | Màn hình hiển thị bếp (Kitchen Display System) real-time qua SSE |
| 💳 **Thanh toán** | Tiền mặt, chuyển khoản, VietQR tự động sinh mã QR |
| 🧾 **In hóa đơn** | Hỗ trợ máy in nhiệt 58mm & 80mm |
| 👥 **Khách hàng** | Quản lý danh sách, lịch sử mua hàng, hạng thành viên |
| 🎁 **Tích điểm & Đổi quà** | Hệ thống loyalty 4 hạng: Đồng → Bạc → Vàng → Kim Cương |
| 🧑‍💼 **Nhân viên & Ca làm** | Quản lý ca, đối soát tiền mặt đầu/cuối ca |
| 📊 **Báo cáo** | Dashboard doanh thu, báo cáo theo ca/ngày/tháng |
| 📦 **Kế toán & Kho** | Thu/chi, nhập hàng, quản lý tồn kho, bảng lương |
| 🔒 **Phân quyền** | 5 vai trò: Admin, Thu ngân, Phục vụ, Bếp, Kế toán |
| 🖥️ **Kiosk mode** | Màn hình khách tự gọi món / customer display |
| 💾 **Backup & Restore** | Xuất/nhập database SQLite |
| 📝 **Audit Log** | Nhật ký toàn bộ thao tác hệ thống |
| 🌐 **Multi-device** | Nhiều thiết bị cùng kết nối, đồng bộ real-time |
| ☁️ **Cloudflare Tunnel** | Truy cập từ xa không cần mở port router |
| 🤖 **AI (Gemini)** | Tích hợp Gemini API (tuỳ chọn) |

---

## 🏗️ Kiến Trúc Hệ Thống / System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                  MÁY CHỦ / SERVER PC                    │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │           CafePOS Server (Express.js)            │   │
│  │  ─────────────────────────────────────────────  │   │
│  │  • REST API (16 modules)                         │   │
│  │  • Realtime SSE (Server-Sent Events)             │   │
│  │  • SQLite Database (sql.js)                      │   │
│  │  • Vite Dev / Static file serving                │   │
│  │  • Network auto-detect (Wi-Fi / Ethernet)        │   │
│  └─────────────────────────────────────────────────┘   │
│                         │                               │
│               Port 3000 / HTTPS Cloudflare              │
└─────────────────────────┬───────────────────────────────┘
                          │
          ┌───────────────┼──────────────────┐
          │               │                  │
   ┌──────▼──────┐  ┌─────▼──────┐  ┌───────▼──────┐
   │  Electron   │  │  Browser   │  │   Tablet /   │
   │  Client App │  │  (Chrome,  │  │  Mobile      │
   │  (Windows)  │  │   Edge…)   │  │  (Waitstaff) │
   └─────────────┘  └────────────┘  └──────────────┘
         LAN / Wi-Fi              Cloudflare Tunnel (Remote)
```

### Stack công nghệ / Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 19, TypeScript, TailwindCSS 4, Vite 8, Framer Motion |
| **Backend** | Node.js, Express 4, TypeScript, tsx |
| **Database** | SQLite via `sql.js` (file-based, embedded, zero-config) |
| **Client App** | Electron 28 (Windows desktop) |
| **Realtime** | Server-Sent Events (SSE) |
| **Auth** | JWT + bcrypt + PIN code |
| **Network** | Auto-detect Wi-Fi/Ethernet, Cloudflare Tunnel support |
| **AI** | Google Gemini API (optional) |

---

## 📁 Cấu Trúc Dự Án / Project Structure

```
POS OS/
├── server.ts                  # Entry point — Express server
├── vite.config.ts             # Vite bundler config
├── tsconfig.json
├── package.json
│
├── server/                    # Backend modules
│   ├── db.ts                  # SQLite database engine
│   ├── auth.ts                # JWT authentication
│   ├── realtime.ts            # SSE hub (real-time events)
│   ├── migrations.ts          # Database migrations
│   ├── seed.ts                # Initial data seeder
│   ├── networkHelper.ts       # Wi-Fi/Ethernet/Cloudflare detection
│   ├── schema.sql             # Database schema
│   └── routes/                # API route handlers (16 modules)
│       ├── authRoutes.ts      # /api/auth
│       ├── menuRoutes.ts      # /api/menu
│       ├── tableRoutes.ts     # /api/tables
│       ├── orderRoutes.ts     # /api/orders
│       ├── kitchenRoutes.ts   # /api/kitchen
│       ├── paymentRoutes.ts   # /api/payments
│       ├── customerRoutes.ts  # /api/customers
│       ├── loyaltyRoutes.ts   # /api/loyalty
│       ├── shiftRoutes.ts     # /api/shifts
│       ├── reportRoutes.ts    # /api/reports
│       ├── accountingRoutes.ts# /api/accounting
│       ├── settingsRoutes.ts  # /api/settings
│       ├── backupRoutes.ts    # /api/backup
│       ├── auditRoutes.ts     # /api/audit
│       ├── kioskRoutes.ts     # /api/kiosk
│       └── networkRoutes.ts   # /api/network
│
├── src/                       # Frontend React app
│   ├── App.tsx                # Root application shell
│   ├── main.tsx
│   ├── types/index.ts         # TypeScript type definitions
│   ├── context/               # React Context providers
│   ├── components/            # UI components by module
│   └── utils/
│
├── client-app/                # Electron desktop client
│   ├── main.js                # Electron main process
│   ├── preload.js             # Secure IPC bridge
│   ├── renderer/
│   │   ├── setup.html         # Connection setup screen
│   │   └── main.html          # Main POS webview
│   └── assets/
│
├── data/                      # Runtime data (auto-generated)
│   ├── cafepos.db             # SQLite database file
│   └── network.json           # Cached network info
│
├── public/                    # Static assets
├── dist/                      # Production build output
├── START_SERVER.cmd           # Quick-launch script (Windows)
└── LAUNCH_SERVER.bat          # Full launcher with Cloudflare support
```

---

## 🚀 Hướng Dẫn Cài Đặt & Chạy Server

### Yêu cầu hệ thống / Requirements

- **OS:** Windows 10/11 (64-bit) *(khuyến nghị)*
- **Node.js:** v20 hoặc mới hơn — [tải tại nodejs.org](https://nodejs.org)
- **RAM:** Tối thiểu 2GB (khuyến nghị 4GB+)
- **Disk:** ~500MB cho node_modules + database

---

### Bước 1 — Clone / Tải dự án

```bash
git clone https://github.com/your-username/cafepos.git
cd cafepos
```

Hoặc giải nén file ZIP vào thư mục bất kỳ.

---

### Bước 2 — Cài dependencies

```bash
npm install
```

---

### Bước 3 — Cấu hình môi trường (tuỳ chọn)

Sao chép file `.env.example` thành `.env`:

```bash
copy .env.example .env
```

Chỉnh sửa `.env` nếu cần:

```env
# Cổng server (mặc định 3000)
PORT=3000

# NODE_ENV: development | production
NODE_ENV=development

# Gemini AI API Key (tuỳ chọn)
GEMINI_API_KEY=your_api_key_here

# Cloudflare Tunnel URL (tuỳ chọn)
CLOUDFLARE_URL=https://your-tunnel.trycloudflare.com
```

---

### Bước 4 — Khởi động Server

#### ✅ Cách nhanh nhất (Windows) — Click đúp vào file:

```
START_SERVER.cmd
```

> Server sẽ tự động khởi động, tạo database, seed dữ liệu mẫu và hiển thị địa chỉ IP.

#### ✅ Dùng terminal:

```bash
# Chế độ Development (có Vite HMR)
npm run dev

# Hoặc
npm start
```

#### ✅ Production (sau khi build):

```bash
# Build frontend
npm run build

# Chạy server production
NODE_ENV=production npm start
```

---

### Bước 5 — Truy cập ứng dụng

Sau khi server chạy, bạn sẽ thấy thông tin tương tự:

```
[CafePOS] Server running at http://localhost:3000
[NETWORK] Wi-Fi IP: 192.168.1.5, Ethernet IP: N/A, Primary: 192.168.1.5
```

Mở trình duyệt và truy cập:

| Thiết bị | URL |
|---------|-----|
| Máy chủ (localhost) | `http://localhost:3000` |
| Thiết bị khác cùng mạng | `http://192.168.1.5:3000` *(thay bằng IP thực)* |
| Màn hình Kiosk | `http://localhost:3000/kiosk` |

---

### ☁️ Kích hoạt Cloudflare Tunnel (Truy cập từ xa)

Cloudflare Tunnel cho phép truy cập CafePOS từ bất kỳ đâu mà **không cần mở port router**:

```bash
# Cài cloudflared (chỉ cần 1 lần)
winget install Cloudflare.cloudflared

# Chạy tunnel (terminal riêng)
cloudflared tunnel --url http://localhost:3000
```

Cloudflare sẽ trả về URL dạng:
```
https://random-name-xyz.trycloudflare.com
```

Copy URL này và điền vào:
- File `.env` → `CLOUDFLARE_URL=https://...`
- Hoặc Client App (Electron) ở màn hình kết nối

---

### 👤 Đăng nhập lần đầu / Default Login

| Field | Giá trị |
|-------|--------|
| Username | `admin` |
| Password | `admin123` |
| Role | ADMIN (toàn quyền) |

> ⚠️ **Hãy đổi mật khẩu admin ngay sau khi đăng nhập lần đầu!**

---

## 💻 Hướng Dẫn Client App (Electron)

**CafePOS Client** là ứng dụng desktop (Windows) giúp kết nối đến server CafePOS qua LAN hoặc Cloudflare Tunnel, hiển thị POS như một ứng dụng native với cửa sổ toàn màn hình, thanh tiêu đề tuỳ chỉnh, và kết nối tự động thông minh.

### 📥 Tải về / Download

| Phiên bản | Nền tảng | Loại | Link tải |
|-----------|---------|------|---------|
| **v1.0.0** | Windows 64-bit | Portable (.zip) | [⬇️ CafePOS-Client-v1.0.0-win64.zip](https://github.com/trietpko2002/Cafe-Pos-Node.js/releases/download/v1.0.0/CafePOS-Client-v1.0.0-win64.zip) |
| **v1.0.0** | Windows 64-bit | Installer (.exe) | [⬇️ CafePOS-Client-Setup-v1.0.0.exe](https://github.com/trietpko2002/Cafe-Pos-Node.js/releases/tag/v1.0.0) |

> 💡 **Khuyến nghị dùng bản Portable (.zip)** — Giải nén và chạy thẳng, không cần cài đặt.
>
> Hoặc xem tất cả phiên bản tại: [**Releases →**](https://github.com/trietpko2002/Cafe-Pos-Node.js/releases)

---

### Cài đặt & Chạy Client (từ source)

```bash
# Chuyển vào thư mục client
cd client-app

# Cài dependencies
npm install

# Chạy app
npm start
```

### Sử dụng Client

1. **Mở app** → Màn hình **"Kết Nối Server"** xuất hiện
2. Nhập **IP LAN** (ví dụ: `http://192.168.1.5:3000`)
3. *(Tuỳ chọn)* Nhập **Cloudflare URL** (`https://xxx.trycloudflare.com`)
4. Nhấn **⚡ Kết Nối Nhanh Nhất** — App tự ping cả 2, chọn cái phản hồi nhanh hơn
5. POS app mở ra trong cửa sổ **toàn màn hình**
6. **Lần sau** mở app sẽ **tự động kết nối lại** server đã lưu

### Build thành file .exe (Portable)

```bash
cd client-app

# Build installer (.exe)
npm run build

# Build + tạo file ZIP luôn
npm run build:zip
```

File xuất ra tại `client-app/dist-build/`

---

## 🎭 Vai Trò & Phân Quyền / Roles & Permissions

| Vai trò | Role Code | Quyền hạn |
|---------|-----------|-----------|
| 👑 Quản trị viên | `ADMIN` | Toàn quyền tất cả module |
| 💰 Thu ngân | `THU_NGAN` | POS, thanh toán, báo cáo ca, khách hàng |
| 🍽️ Phục vụ | `PHUC_VU` | Gọi món, xem bàn, ghi chú order |
| 👨‍🍳 Bếp | `BEP` | Màn hình bếp KDS (chỉ xem & cập nhật trạng thái) |
| 📒 Kế toán | `KE_TOAN` | Kế toán, kho hàng, bảng lương |

---

## 🔄 Cách Hoạt Động / How It Works

### Luồng bán hàng cơ bản / Basic Sales Flow

```
[Phục vụ / Waiter]
      │
      ▼
Chọn bàn trên TableMap
      │
      ▼
POS Screen: Chọn sản phẩm → Tuỳ chỉnh (size, đường, đá, topping)
      │
      ▼
Gửi đơn → Server lưu DB → SSE broadcast "new_order"
      │                            │
      │                            ▼
      │                   [Bếp nhận lệnh - KDS]
      │                   Cập nhật trạng thái
      │                   PREPARING → READY → SERVED
      │
      ▼
[Thu ngân] Thanh toán
      │
      ├── Tiền mặt (ghi nhận, cân đối ca)
      ├── Chuyển khoản ngân hàng
      └── VietQR (sinh mã QR tự động)
            │
            ▼
      In hoá đơn 58/80mm → Đóng đơn → Cập nhật bàn → Cộng điểm khách hàng
```

### Real-time Sync

- Server sử dụng **Server-Sent Events (SSE)** tại `/api/realtime/stream`
- Khi có thay đổi (đơn mới, cập nhật bàn, trạng thái bếp…), server **push event** đến tất cả client đang kết nối
- Mỗi client lắng nghe và **tự cập nhật UI** mà không cần reload trang

---

## 🌐 API Endpoints Tổng Quan / API Overview

| Module | Base URL | Chức năng |
|--------|----------|-----------|
| Auth | `/api/auth` | Đăng nhập, đăng xuất, thông tin user |
| Menu | `/api/menu` | Danh mục, sản phẩm, size, topping |
| Tables | `/api/tables` | Quản lý bàn, khu vực |
| Orders | `/api/orders` | Tạo/sửa/huỷ đơn hàng |
| Kitchen | `/api/kitchen` | KDS — cập nhật trạng thái chế biến |
| Payments | `/api/payments` | Thanh toán, VietQR |
| Customers | `/api/customers` | Quản lý khách hàng |
| Loyalty | `/api/loyalty` | Tích điểm, đổi quà, hạng thành viên |
| Shifts | `/api/shifts` | Quản lý ca làm việc |
| Reports | `/api/reports` | Báo cáo doanh thu |
| Accounting | `/api/accounting` | Kế toán, kho, bảng lương |
| Settings | `/api/settings` | Cài đặt cửa hàng |
| Backup | `/api/backup` | Xuất/nhập database |
| Audit | `/api/audit` | Nhật ký thao tác |
| Kiosk | `/api/kiosk` | Màn hình kiosk khách hàng |
| Network | `/api/network` | Thông tin mạng / Cloudflare |
| Realtime | `/api/realtime/stream` | SSE stream (real-time events) |

---

## 🖨️ Cài Đặt Máy In / Printer Setup

CafePOS hỗ trợ máy in nhiệt USB/Bluetooth/LAN:

1. Đăng nhập **ADMIN** → **Cài đặt → Máy in**
2. Chọn khổ giấy: **58mm** hoặc **80mm**
3. Bật/tắt: tự động in, logo, thông tin WiFi, điểm tích luỹ khách hàng
4. Nhập ghi chú footer hoá đơn tuỳ ý

> Máy in phải được cài driver và chia sẻ qua mạng LAN, hoặc cắm USB trực tiếp vào máy chủ.

---

## 💰 Donate / Ủng Hộ Tác Giả

Nếu bạn thấy **CafePOS** hữu ích và muốn ủng hộ để dự án tiếp tục phát triển:


---

### 🏦 VietQR / Chuyển khoản ngân hàng

```
Ngân hàng   : BIDV
Số TK       : 6160284592
Chủ TK      : VO NGUYEN NHAT TRIET
Nội dung CK : DONATE CAFEPOS
```

*(Quét mã VietQR hoặc chuyển khoản theo thông tin trên)*

---

### 📱 MoMo

```
SĐT MoMo: [Số điện thoại MoMo của bạn]
Ghi chú : DONATE CAFEPOS
```

Mọi đóng góp dù nhỏ đều rất có ý nghĩa và giúp dự án phát triển tốt hơn! 🙏

---

## 👨‍💻 Tác Giả / Author

<div align="center">

**Triet Vo**

Passionate developer building practical tools for Vietnamese F&B businesses.

[![GitHub](https://img.shields.io/badge/GitHub-@trietpko2002-181717?style=flat-square&logo=github)](https://github.com/trietpko2002)

*"Làm ra những thứ thực sự hữu ích cho người Việt"*

</div>

---

## 📜 License

```
MIT License — Copyright (c) 2026 Triet Vo

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

---

## 🤝 Đóng Góp / Contributing

Pull requests và issue reports đều được chào đón! Nếu bạn muốn đóng góp:

1. **Fork** dự án
2. Tạo branch mới: `git checkout -b feature/ten-tinh-nang`
3. Commit: `git commit -m 'feat: thêm tính năng xyz'`
4. Push: `git push origin feature/ten-tinh-nang`
5. Mở **Pull Request**

---

## ❓ FAQ — Câu Hỏi Thường Gặp

**Q: Server có cần Internet không?**
A: Không. CafePOS chạy hoàn toàn offline trên mạng LAN. Chỉ cần Internet nếu dùng Cloudflare Tunnel hoặc Gemini AI.

**Q: Dữ liệu lưu ở đâu?**
A: File `data/cafepos.db` — SQLite database cục bộ trên máy chủ. Có thể backup/restore qua giao diện Admin.

**Q: Có thể dùng trên macOS/Linux không?**
A: Server có thể chạy trên mọi hệ điều hành có Node.js. Electron Client hiện build cho Windows; macOS và Linux đang xem xét.

**Q: Bao nhiêu thiết bị có thể kết nối cùng lúc?**
A: Không giới hạn cứng — phụ thuộc tốc độ mạng LAN và hiệu năng máy chủ. Thực tế 10–20 thiết bị cùng lúc hoạt động tốt.

**Q: Làm sao thêm sản phẩm/menu?**
A: Đăng nhập ADMIN → **Quản lý Menu** → Thêm danh mục và sản phẩm. Hỗ trợ upload ảnh, nhiều size, topping.

**Q: VietQR hoạt động như thế nào?**
A: Điền thông tin ngân hàng trong **Cài đặt → Thanh toán**. Khi thu ngân chọn "Chuyển khoản", hệ thống tự sinh mã QR với số tiền chính xác theo chuẩn VietQR.

---

<div align="center">

Made with ❤️ in Vietnam 🇻🇳 by **Triet Vo**

*Nếu thấy hữu ích, hãy ⭐ Star dự án để ủng hộ nhé!*

</div>

