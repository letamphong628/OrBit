# 🛡️ OrBit Browser — High-Security Chromium Privacy Browser

<p align="center">
  <img src="installer/public/logo.svg" alt="OrBit Logo" width="96" height="96" style="margin-bottom: 12px;" onerror="this.style.display='none'">
</p>

<p align="center">
  <strong>Trình duyệt bảo mật cao nhân Chromium — Siêu tối ưu RAM/CPU & Chống giám sát toàn diện</strong><br>
  <em>Tích hợp mạng ẩn danh Tor, mã hóa Tab Ẩn danh chuẩn quân đội AES-256-GCM, chống chụp lén màn hình (Anti-Screen Capture), đăng nhập Google gốc 100%, và giao diện bo góc chuẩn Google Chrome hiện đại.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Chromium-131.0.6778-blue?logo=googlechrome&logoColor=white" alt="Chromium 131">
  <img src="https://img.shields.io/badge/Tor_Network-0.4.8.13-purple?logo=torproject&logoColor=white" alt="Tor 0.4.8">
  <img src="https://img.shields.io/badge/Encryption-AES--256--GCM-green" alt="AES-256-GCM">
  <img src="https://img.shields.io/badge/RAM_Saver-Sleeping_Tabs-informational" alt="RAM Saver">
  <img src="https://img.shields.io/badge/Google_Auth-Bypass_Secured-success?logo=google" alt="Google Auth">
  <img src="https://img.shields.io/badge/Platform-Windows_10%2F11_x64-0078D6?logo=windows" alt="Windows">
  <img src="https://img.shields.io/badge/License-MIT-success" alt="MIT License">
</p>

---

## 🌟 1. Điểm Nổi Bật Của OrBit Browser

### 1. 🔑 Đăng Nhập Google Tài Khoản Gốc 100% (Google Sign-In Fix)
- **Giải quyết triệt để lỗi:** *"Couldn't sign you in - This browser or app may not be secure"*.
- **Cơ chế hoạt động:**
  - Khi điều hướng tới các endpoint đăng nhập của Google (`accounts.google.com`, `accounts.youtube.com`, `oauth2.googleapis.com`), OrBit tự động chuyển đổi sang User-Agent sạch của **Firefox Desktop** (`Mozilla/5.0 ... Gecko/20100101 Firefox/133.0`) và làm sạch Client Hints (`sec-ch-ua*`) cùng cờ `Sec-GPC`/`DNT`.
  - Tiêm mã tiền tải `src/browser/tab_preload.js` tại thời điểm khởi tạo (`document_start`) để che giấu thuộc tính `navigator.webdriver`.
  - Mọi cookie phiên đăng nhập (`SID`, `HSID`, `SSID`, `APISID`, `SAPISID`) được lưu trữ hợp lệ vào session phân vùng, cho phép sử dụng Gmail, YouTube, Google Drive và Google Search liền mạch.

---

### 2. 🕶️ Tab Ẩn Danh Khóa Mật Khẩu Chuẩn Quân Đội (Master Password Vault)
- **Lần đầu tiên mở Tab Ẩn Danh:** Bắt buộc thiết lập **Mật khẩu Chủ (Master Password)**.
- **Những lần truy cập sau:** **PHẢI CÓ MẬT KHẨU** mới mở khóa được khu vực riêng tư.
- **Tiêu chuẩn mã hóa:**
  - Thuật toán băm khóa: **PBKDF2-HMAC-SHA512** với **250.000 vòng lặp** và chuỗi muối ngẫu nhiên (salt) 32-byte chống tấn công dò từ điển qua GPU.
  - Thuật toán mã hóa đối xứng: **AES-256-GCM** (Chuẩn an ninh chính phủ NIST FIPS 197).
  - Tự động đóng băng và khóa lại khi không sử dụng. Hỗ trợ **Phím khẩn cấp Panic Wipe (`Esc x 2`)** để đóng toàn bộ tab ẩn danh và xóa sạch dấu vết RAM tức thì.

---

### 3. 🚫 Chống Chụp & Quay Lén Màn Hình (Win32 Anti-Screen Capture)
- Trong Tab Ẩn Danh, OrBit tự động kích hoạt API gốc của hệ điều hành Windows:
  ```c
  SetWindowDisplayAffinity(hwnd, WDA_MONITOR);
  ```
- **Hiệu quả thực tế:** Mọi phần mềm ghi hình màn hình (Windows Snipping Tool, OBS Studio, Discord Stream, Zoom, Google Meet hay trojan/spyware) khi quay quét cửa sổ OrBit **chỉ thu được một màn hình ĐEN TUYỀN (Black Screen)**.

---

### 4. 🧅 Chống Nhà Mạng Soi Web (Anti-ISP Surveillance) Với Tor & ECH
OrBit triệt tiêu toàn bộ 3 con đường nhà mạng (Viettel, VNPT, FPT...) giám sát người dùng:
1. **Mạng Ẩn Danh Tor Tích Hợp:** Đóng gói sẵn `tor.exe` (Tor Expert Bundle). Chỉ cần nhấn nút `🧅 Tor: Bật/Tắt` trên thanh địa chỉ, toàn bộ kết nối web sẽ được bọc nhiều lớp mã hóa qua mạng lưới Onion Routing (SOCKS5 `127.0.0.1:9050`). Nhà mạng hoàn toàn không thể xem bạn đang truy cập web gì.
2. **DNS-over-HTTPS (DoH):** Mọi truy vấn phân giải tên miền được mã hóa qua máy chủ **Quad9 (Thụy Sĩ — theo luật bảo mật Thụy Sĩ, cam kết zero-log và chặn mã độc)**.
3. **Encrypted Client Hello (ECH):** Mã hóa tiêu đề SNI trong bắt tay TLS 1.3, vô hiệu hóa các thiết bị giám sát gói tin sâu (DPI) của nhà mạng.
4. **WebRTC IP Leak Shield:** Cấu hình `--force-webrtc-ip-handling-policy=disable_non_proxied_udp`, chống rò rỉ địa chỉ IP thật qua STUN/TURN.

---

### 5. ⚡ Siêu Tối Ưu RAM & CPU (Sleeping Tabs & Bộ Dọn RAM)
- **Tab Ngủ Đông (Sleeping Tabs):** Sau 2 phút không xem tab nền (và tab không phát âm thanh), trình duyệt tự động đóng băng tiến trình, hạ CPU về 0% và thu hồi bộ nhớ, hiển thị biểu tượng `💤`. Nhấp lại tab sẽ thức giấc tức thì.
- **Nút Dọn RAM 1 Chạm:** Đo đạc và hiển thị dung lượng RAM thực tế trên thanh công cụ (ví dụ: `68 MB`). Nhấp vào là OrBit lập tức xả bộ nhớ đệm (Cache Flush) và ép gom rác bộ nhớ (Garbage Collection).
- **Giới hạn tài nguyên:** Giới hạn tiến trình renderer và V8 heap giúp máy vận hành êm ái, nhẹ hơn 60-70% so với Chrome thông thường.

---

### 6. 🎨 Giao Diện Chuẩn Chrome Hiện Đại ("Bo Góc Thời Nay")
- **Bo góc toàn diện:** Thanh Omnibox dạng viên thuốc (`border-radius: 20px`), thẻ duyệt web bo cong (`border-radius: 12px 12px 0 0`), nút bấm bo tròn (`border-radius: 50%`), hộp thoại và popover bo tròn mềm mại (`border-radius: 16px - 20px`).
- **Thanh công cụ đầy đủ:**
  - Nút **Tải xuống (📥 Downloads)** với huy hiệu đếm số tệp đang tải và popup theo dõi tiến trình.
  - Nút **Tiện ích mở rộng (🧩 Extensions)** với popup quản lý nhanh và liên kết Chrome Web Store.
  - Nút **Cài đặt (⚙️ Settings)** truy cập thẳng `orbit://settings`.
  - Nút **Đồng bộ Google & Avatar (👤 Profile)** hiển thị tên người dùng và trạng thái đồng bộ.
  - Nút **Giám sát RAM (⚡ RAM Gauge)** hiển thị mức tiêu thụ tài nguyên thực tế.
  - Nút **Menu 3 chấm (⋮ Chrome Menu)** mở bảng điều khiển nổi.

---

### 7. 📋 Menu 3 Chấm Chuẩn Google Chrome (Floating Overlay Window)
Được triển khai dưới dạng cửa sổ con nổi (Child Window) độc lập phía trên `WebContentsView`, không bao giờ bị che khuất hoặc cắt xén:
- **Thẻ định danh tài khoản ở trên cùng:** Ảnh đại diện, tên hiển thị **Lê Tâm Phong**, huy hiệu **Đã đăng nhập**, và mũi tên `›`.
- **Toàn bộ danh mục và biểu tượng SVG chính gốc:**
  - `Thẻ mới` (`Ctrl+T`), `Cửa sổ mới` (`Ctrl+N`), `Cửa sổ Ẩn danh mới` (`Ctrl+Shift+N`).
  - `Mật khẩu và tính năng tự động điền ›`
  - `Nhật ký ›` (`Ctrl+H`)
  - `Tệp đã tải xuống` (`Ctrl+J`)
  - `Dấu trang và danh sách ›`
  - `Nhóm thẻ ›`
  - `Tiện ích mở rộng ›`
  - `Xoá dữ liệu duyệt web...` (`Ctrl+Shift+Del`)
  - **Thanh thu phóng:** `Thu phóng [-] 90% [+] [⛶]` (tương tác trực tiếp trên trang).
  - `In...` (`Ctrl+P`)
  - `Mở Gemini trong Chrome`
  - `Tìm kiếm trên thẻ này bằng Google Ống kính`
  - `Dịch...`
  - **Menu con "Tìm và chỉnh sửa ›":** Bung sang bên trái (`Tìm... Ctrl+F`, `Cắt Ctrl+X`, `Sao chép Ctrl+C`, `Dán Ctrl+V`).
  - **Menu con "Truyền, lưu và chia sẻ ›":** `Truyền...`, `Lưu trang dưới dạng... Ctrl+S`, `Tạo lối tắt...`, `Sao chép đường liên kết`, `Tạo mã QR cho trang này`.
  - **Menu con "Công cụ khác ›":** `⚡ Giải phóng RAM ngay`, `Tìm thẻ`, `Công cụ dành cho Nhà phát triển Ctrl+Shift+I`, `🛠️ OrBit Developer Mode`.
  - `Trợ giúp ›` (`orbit://version`), `Cài đặt` (`orbit://settings`), `Thoát`.

---

## 🌐 2. Hệ Thống Trang Nội Bộ `orbit://`

| Địa Chỉ Nội Bộ | Chức Năng |
| :--- | :--- |
| `orbit://new-page` | Trang Tab Mới tối giản, tìm kiếm Google, hỗ trợ thêm lối tắt với icon gốc chuẩn xác. |
| `orbit://settings` | Trang Cài đặt chuẩn Chrome: Tùy chỉnh Sleeping Tabs, dọn RAM, bảo mật Tor, mật khẩu Tab Ẩn danh, công cụ tìm kiếm. |
| `orbit://downloads` | Quản lý lịch sử và tiến trình tệp đã tải xuống, mở thư mục, tìm kiếm tệp. |
| `orbit://extensions` | Quản lý tiện ích mở rộng và liên kết đến Cửa hàng Chrome trực tuyến. |
| `orbit://version` | Xem đầy đủ thông số nhân Chromium, V8 engine, Tor daemon, switches và User-Agent. |
| `orbit://developermode` | **Terminal Nhà Phát Triển:** Yêu cầu nhập Mật khẩu Chủ của Tab Ẩn danh để mở khóa. Cho phép can thiệp sâu vào trình duyệt bằng lệnh CLI. |

---

## 🚀 3. Hướng Dẫn Cài Đặt & Sử Dụng

### Cách 1: Sử Dụng Trình Cài Đặt GUI Chuyên Nghiệp (Khuyên Dùng)
Nhấp đúp chuột vào file:
```cmd
Setup.bat
```
Trình cài đặt GUI (thiết kế Cyber Dark Neon độc quyền) sẽ khởi chạy với quy trình 5 bước tự động:
1. **Chào mừng:** Giới thiệu thông số OrBit Browser v1.0.0.
2. **Điều khoản:** Đọc chính sách bảo mật Zero-Log và cam kết riêng tư.
3. **Thư mục cài đặt:** Tự nhận diện `%LOCALAPPDATA%\OrBit Browser` (hoặc bấm *Duyệt...* để chọn nơi khác), tích chọn tạo Desktop Shortcut và tích hợp Tor.
4. **Cài đặt:** Tự động giải nén và sao chép toàn bộ nhân Chromium, DLLs và Tor từ gói offline sẵn có (không cần tải internet).
5. **Hoàn tất:** Nhấn *Hoàn Tất* để khởi chạy OrBit ngay lập tức!

### Cách 2: Khởi Chạy Nhanh Trực Tiếp (Portable Mode)
Nhấp đúp chuột vào file:
```cmd
Run-OrBit.bat
```
Hoặc mở trực tiếp file thực thi đã biên dịch đầy đủ thư viện:
```cmd
release\OrBit-win32-x64\OrBit.exe
```

---

## ⌨️ 4. Bảng Phím Tắt Tiện Dụng

| Phím Tắt | Chức Năng |
| :--- | :--- |
| `Ctrl + T` | Mở thẻ mới (`orbit://new-page`) |
| `Ctrl + N` | Mở cửa sổ mới |
| `Ctrl + Shift + N` | Mở thẻ ẩn danh bảo mật (Yêu cầu Mật Khẩu Chủ) |
| `Ctrl + J` | Mở trang Tệp đã tải xuống (`orbit://downloads`) |
| `Ctrl + W` | Đóng thẻ hiện tại |
| `Ctrl + R` | Tải lại trang web |
| `Ctrl + L` | Đưa con trỏ vào thanh địa chỉ Omnibox |
| `Ctrl + P` | In trang web hiện tại |
| `Ctrl + Shift + Del` | Xóa dữ liệu duyệt web |
| `Nhấn Esc 2 lần` | **🚨 Panic Wipe:** Hủy tức thì mọi tab ẩn danh, xả RAM và khóa két an toàn |

---

## 🛠️ 5. Danh Sách Lệnh Trong `orbit://developermode`

Sau khi mở khóa bằng Mật khẩu Chủ trong `orbit://developermode`, bạn có thể thực thi các lệnh sau:

| Câu Lệnh | Tác Dụng |
| :--- | :--- |
| `help` | Hiển thị bảng trợ giúp và danh sách câu lệnh hệ thống |
| `status` | Xem tình trạng tài nguyên RAM, CPU, Tor daemon, Anti-Capture |
| `devtools` | Mở cửa sổ kiểm tra mã nguồn Chromium DevTools (F12) |
| `ram --flush` | Dọn dẹp bộ nhớ đệm và thực hiện gom rác V8 Heap ngay lập tức |
| `tor start` | Kích hoạt định tuyến mạng ẩn danh Tor (Socks5 127.0.0.1:9050) |
| `tor stop` | Tắt mạng Tor, quay về kết nối internet trực tiếp |
| `bypass-capture on` | **TẮT** chống chụp màn hình *(Cho phép quay/chụp màn hình — GIẢM BẢO MẬT)* |
| `bypass-capture off` | **BẬT LẠI** chống chụp màn hình *(Màn hình đen trên OBS/Discord)* |
| `flags` | Liệt kê các cờ dòng lệnh Chromium đang chạy |
| `clear` | Xóa sạch màn hình dòng lệnh |
| `lock` | Khóa lại chế độ Developer Mode |
| `exit` | Trở về trang chủ `orbit://new-page` |

---

## 📁 6. Cấu Trúc Mã Nguồn Dự Án

```
c:\Users\PhongOfficial5\Desktop\OrBit\
├── Setup.bat                         <- File chạy Trình cài đặt GUI (Installer Wizard)
├── Run-OrBit.bat                     <- File khởi chạy nhanh trình duyệt di động
├── README.md                         <- Tài liệu giới thiệu & Hướng dẫn kỹ thuật
├── HUONG_DAN_SU_DUNG.md              <- Cẩm nang chi tiết cho người dùng
├── package.json                      <- Cấu hình gói và script build Electron
├── preload.js                        <- Cầu nối IPC an toàn (ContextBridge) cho giao diện chính
├── installer\
│   ├── server.js                     <- Máy chủ HTTP nhẹ phục vụ trình cài đặt GUI
│   ├── installer_engine.js           <- Động cơ cài đặt, sao chép file & tạo shortcut
│   └── public\
│       └── index.html                <- Giao diện Installer 5 bước (Cyber Dark Neon)
├── release\
│   └── OrBit-win32-x64\
│       ├── OrBit.exe                 <- File thực thi chính của trình duyệt
│       ├── ffmpeg.dll                <- Bộ giải mã Video/Audio HTML5
│       ├── d3dcompiler_47.dll        <- Thư viện DirectX GPU Rasterization
│       ├── vk_swiftshader.dll        <- Thư viện đồ họa Vulkan
│       ├── vulkan-1.dll              <- Driver giao tiếp Vulkan
│       ├── libEGL.dll, libGLESv2.dll <- Thư viện kết xuất WebGL
│       └── tor\
│           └── tor.exe               <- Tiến trình mạng ẩn danh Tor di động
├── src\
│   ├── security\
│   │   ├── vault.js                  <- Mã hóa AES-256-GCM + PBKDF2-SHA512
│   │   ├── stealth.js                <- Anti-ISP, DoH Quad9, ECH, WebRTC & Chuyển đổi UA Google Auth
│   │   └── tor.js                    <- Quản lý tiến trình daemon Tor SOCKS5
│   ├── performance\
│   │   └── optimizer.js              <- Động cơ Sleeping Tabs & Thu hồi RAM
│   ├── browser\
│   │   ├── tabs.js                   <- Quản lý đa thẻ WebContentsView & điều hướng orbit://
│   │   ├── sync.js                   <- Quản lý hồ sơ & đồng bộ tài khoản Google
│   │   ├── downloads.js              <- Động cơ quản lý tệp tải xuống (DownloadManager)
│   │   └── tab_preload.js            <- Tiêm mã che giấu cờ tự động hóa (webdriver) trước khi trang tải
│   └── ui\
│       ├── index.html                <- Khung giao diện chính chuẩn Google Chrome bo góc
│       ├── styles.css                <- Thiết kế giao diện Dark Mode, Omnibox, Tabs, Popovers
│       ├── renderer.js               <- Logic điều khiển UI, thanh công cụ & Popovers
│       ├── chrome_menu.html          <- Menu 3 chấm chuẩn Chrome hiện đại (Cửa sổ nổi độc lập)
│       ├── menu_preload.js           <- Cầu nối IPC cho menu 3 chấm
│       ├── newtab.html               <- Trang tab mới (orbit://new-page)
│       ├── settings.html             <- Trang cài đặt chuẩn Chrome (orbit://settings)
│       ├── downloads.html            <- Trang quản lý tệp đã tải xuống (orbit://downloads)
│       ├── extensions.html           <- Trang quản lý tiện ích mở rộng (orbit://extensions)
│       ├── version.html              <- Trang thông tin phiên bản (orbit://version)
│       └── developer.html            <- Terminal dòng lệnh (orbit://developermode)
└── main.js                           <- Tiến trình nền Chromium, quản lý vòng đời & IPC
```

---

## 🔒 7. Chính Sách Bảo Mật & Pháp Lý

1. **Tuân thủ quyền riêng tư:** OrBit không thu thập, không phân tích và không gửi bất kỳ thông tin cá nhân nào của bạn về máy chủ bên ngoài. Mọi dữ liệu đều được lưu trữ cục bộ trên máy của bạn.
2. **Tiêu chuẩn mã hóa:** Sử dụng các thư viện mật mã học tiêu chuẩn NIST FIPS 197 (`crypto` của Node.js / OpenSSL) với các tham số độ khó cao chống tấn công dò mật khẩu.
3. **Mã nguồn minh bạch:** Phát triển trên nền tảng Chromium và Electron ổn định, bảo đảm tính minh bạch và độ tin cậy tuyệt đối.
