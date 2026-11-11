# HƯỚNG DẪN SỬ DỤNG TRÌNH DUYỆT CHROME ORBIT
**Trình duyệt giao diện chuẩn Chrome nhân Chromium - Tích hợp mạng ẩn danh Tor & Tối ưu RAM**

---

## 🚀 1. Cách Khởi Động Trình Duyệt

Có 2 cách rất nhanh để chạy trình duyệt ngay trong thư mục dự án:
- **Cách 1 (Nhanh nhất):** Nhấp đúp chuột vào file:
  ```
  Run-OrBit.bat
  ```
  *(Nằm ngay tại thư mục gốc `c:\Users\PhongOfficial5\Desktop\OrBit\`)*
- **Cách 2:** Mở trực tiếp file thực thi đã build đầy đủ `.dll` và `tor.exe`:
  ```
  release\OrBit-win32-x64\OrBit.exe
  ```

---

## 🌟 2. Các Thay Đổi & Tính Năng Mới Cập Nhật

### 1. Giao Diện Chuẩn Google Chrome (Không Bản Quyền)
- **Xóa bỏ các huy hiệu trạng thái cũ:** Giao diện trang New Tab hoàn toàn sạch sẽ, thanh lịch chuẩn Chrome gốc.
- **Icon chuẩn gốc:** Toàn bộ icon phím tắt (Google, YouTube, GitHub) được thay bằng **Vector SVG chính hãng** với đúng mã màu thương hiệu gốc, không dùng emoji hay icon tự ý.
- **Thêm lối tắt (+):** Nút tròn "+" chuẩn Chrome cho phép bạn thêm bất kỳ trang web yêu thích nào (nhập Tên + URL) và tự động lưu lại. Rê chuột vào lối tắt sẽ có nút xóa "✕".
- **Thanh đầu trang Google:** Có đầy đủ link "Gmail", "Hình ảnh", nút 9 dấu chấm mở danh mục Google Apps (Tìm kiếm, YouTube, Gmail, Drive, Lịch, GitHub), cùng nút "Đăng nhập" tài khoản Google.
- **Thanh dấu trang (Bookmarks Bar):** Nằm ngay dưới thanh Omnibox chuẩn Chrome, hiển thị nhanh Google, YouTube, GitHub, Gmail và thư mục "Dấu trang khác".
- **Màn hình Chào mừng (First-Run Experience):** Khi mở trình duyệt lần đầu, một cửa sổ chào mừng chuẩn Chrome sẽ xuất hiện hướng dẫn trải nghiệm.

### 2. Bảo Mật Toàn Diện Với Mạng Ẩn Danh TOR
- Đã đóng gói bộ **Tor Expert Bundle (tor.exe)** chạy ngầm di động ngay trong thư mục `tor/`.
- Nút kích hoạt nhanh hình củ hành **🧅 Tor** ngay trên thanh địa chỉ Omnibox và trong Menu 3 chấm:
  - Khi bật Tor: Toàn bộ lưu lượng truy cập web, câu hỏi DNS và bắt tay TLS được định tuyến qua mạng lưới Onion Routing của Tor (SOCKS5 `127.0.0.1:9050`).
  - **Nhà mạng (ISP) hoàn toàn KHÔNG THỂ biết bạn đang vào trang web nào, xem gì hay tải gì.**
  - Kết hợp với **ECH (Encrypted Client Hello)** và **WebRTC Shield** chống rò rỉ IP.

### 3. Đồng Bộ Hóa Google Y Chang Chrome
- Nút Avatar tài khoản ở góc phải thanh công cụ.
- Nhấp vào sẽ mở ra thẻ hồ sơ:
  - "Tính năng đồng bộ hóa Chrome"
  - Đăng nhập tài khoản Google gốc (`accounts.google.com`) an toàn, không bị Google chặn.
  - Lưu giữ thông tin hồ sơ và đồng bộ cài đặt.

### 4. Tab Ẩn Danh Yêu Cầu Mật Khẩu Chủ & Chống Chụp Màn Hình
- Lần đầu mở Tab Ẩn Danh: Thiết lập **Mật khẩu Chủ (Master Password)**.
- Mọi lần mở sau: **BẮT BUỘC có mật khẩu** mới vào được.
- Mã hóa: **AES-256-GCM + PBKDF2-HMAC-SHA512** (250,000 vòng lặp).
- Chống quay/chụp lén màn hình: `SetWindowDisplayAffinity(WDA_MONITOR)` - Snipping Tool, OBS, Discord chỉ thấy màn hình ĐEN TUYỀN.
- Phím tắt khẩn cấp: Nhấn `Esc` 2 lần liên tiếp để kích hoạt **🚨 Panic Wipe** hủy toàn bộ tab ẩn danh tức thì.

---

## 🛡️ 2. Các Tính Năng Đột Phá Đã Được Tích Hợp

### 1. Tab Ẩn Danh Yêu Cầu Mật Khẩu Chủ (Master Password Vault)
- **Lần đầu tiên sử dụng Tab Ẩn Danh:** Trình duyệt sẽ yêu cầu bạn thiết lập một **Mật khẩu Chủ (Master Password)**.
- **Những lần sau:** Mỗi khi bạn muốn mở hoặc truy cập lại Tab Ẩn Danh, trình duyệt **BẮT BUỘC bạn phải nhập đúng Mật khẩu Chủ** thì mới mở khóa.
- **Chuẩn mã hóa quân đội:**
  - Thuật toán băm khóa: **PBKDF2-HMAC-SHA512** với **250,000 vòng lặp** và chuỗi muối ngẫu nhiên (salt) 32-byte bảo vệ chống dò mật khẩu bằng siêu máy tính hoặc GPU.
  - Thuật toán mã hóa xác thực: **AES-256-GCM** (chuẩn FIPS 197 của chính phủ Hoa Kỳ).
  - Tự động đóng băng và khóa lại khi không hoạt động hoặc khi nhấn nút **🚨 Panic Wipe (Esc x 2)**.

### 2. Chống Chụp & Quay Lén Màn Hình (Win32 Anti-Screen Capture)
- Trong Tab Ẩn Danh, trình duyệt tự động gọi hàm API cấp thấp của Windows:
  `SetWindowDisplayAffinity(hwnd, WDA_MONITOR)`
- **Kết quả:** Bất kỳ phần mềm chụp màn hình nào (Windows Snipping Tool, OBS Studio, Discord Stream, Zoom, Google Meet hay trojan/spyware chạy ngầm) khi quay hoặc chụp cửa sổ OrBit **chỉ thu được một màn hình ĐEN hoàn toàn**.

### 3. Nghiên Cứu & Triển Khai Chống Nhà Mạng (ISP) Soi Lịch Sử Web
Nhà mạng thường giám sát bạn qua 3 con đường:
1. **Soi tên miền qua cổng DNS Port 53:** Nhà mạng thấy mọi trang web bạn gõ.
   - **Giải pháp của OrBit:** Kích hoạt chế độ **DNS-over-HTTPS (DoH)** thông qua hệ thống máy chủ **Quad9 (Thụy Sĩ - theo luật bảo mật Thụy Sĩ, cam kết zero-log và chặn mã độc)** cùng Cloudflare. Toàn bộ câu hỏi DNS được mã hóa bằng TLS 1.3, nhà mạng không thể đọc được.
2. **Soi tên miền qua tiêu đề SNI (Server Name Indication) trong bắt tay TLS:**
   - **Giải pháp của OrBit:** Kích hoạt tính năng **ECH (Encrypted Client Hello)** của Chromium. Tên miền bạn truy cập được mã hóa từ trước khi gói tin rời khỏi máy tính. Thiết bị kiểm duyệt DPI của nhà mạng không thể biết bạn đang vào trang web nào.
3. **Lộ IP qua WebRTC:**
   - **Giải pháp của OrBit:** Cấu hình chính sách `--force-webrtc-ip-handling-policy=disable_non_proxied_udp`, chặn triệt để mọi hành vi lén gửi IP thực qua STUN/TURN queries.

### 4. Cực Kỳ Tối Ưu RAM & CPU (Sleeping Tabs & Process Throttling)
- **Công nghệ Tab Ngủ Đông (Sleeping Tabs):** Sau 2 phút bạn không chuyển vào một tab chạy ngầm (nếu tab đó không phát âm thanh), trình duyệt tự động hạ mức chiếm dụng CPU về 0% và thu hồi bộ nhớ, hiển thị biểu tượng `💤`.
- **Nút Dọn RAM 1 Chạm:** Trên thanh công cụ có nút đo RAM thời gian thực (ví dụ `85 MB`). Bạn chỉ cần nhấn vào là OrBit sẽ ép dọn bộ nhớ đệm (Cache Flush) và giải phóng RAM ngay lập tức.
- **Giới hạn Render Process:** Cấu hình V8 Engine `--js-flags="--max-old-space-size=256"` và giới hạn tiến trình giúp máy tính luôn mượt mà.

### 5. Giao Diện Chuẩn Chrome & Đăng Nhập Google Gốc
- Thiết kế thanh Tab cong chuẩn Chrome, thanh Omnibox có biểu tượng khóa bảo mật, nút Trang chủ, Quay lại, Tải lại.
- **Đăng nhập Google:** Sử dụng User-Agent chính hãng của Google Chrome Desktop mới nhất cùng cờ `disable-blink-features: AutomationControlled`, cho phép bạn đăng nhập tài khoản Google (`accounts.google.com`), YouTube, Drive, Gmail mượt mà, không bao giờ bị báo lỗi "Trình duyệt không an toàn" như các webview thông thường.

---

## 🌐 3. Hệ Thống Địa Chỉ Nội Bộ Chuẩn OrBit (`orbit://`)

Giống như Chrome có `chrome://version`, OrBit sở hữu hệ thống URL nội bộ độc quyền:

| URL Nội Bộ | Mô Tả & Chức Năng |
| :--- | :--- |
| `orbit://new-page` | Trang Tab Mới chính thức, tích hợp tìm kiếm Google, lối tắt và đồng bộ |
| `orbit://version` | Xem toàn bộ thông tin phiên bản OrBit, Chromium, V8, Tor, ECH và User Agent |
| `orbit://developermode` | **Chế độ Nhà Phát Triển (CMD Terminal):** Yêu cầu nhập Mật Khẩu Tab Ẩn Danh để mở khóa. Cho phép gõ lệnh can thiệp hệ thống |

---

## 🛠️ 4. Chế Độ Nhà Phát Triển (`orbit://developermode`)

Khi bạn nhập `orbit://developermode` vào thanh địa chỉ:
1. **Khóa Mật Khẩu An Toàn:** Trình duyệt sẽ yêu cầu nhập đúng **Mật Khẩu Chủ của Tab Ẩn Danh**. Nếu không có mật khẩu, không ai có thể truy cập vào Developer Mode.
2. **Cảnh Báo Bảo Mật:** Cảnh báo người dùng rằng các thao tác tại đây có thể can thiệp sâu vào nhân Chromium và làm giảm mức độ an ninh nếu tắt bảo vệ.
3. **Giao Diện Terminal / CMD Chuyên Nghiệp:**
   Khi gõ lệnh `help` và nhấn `Enter`, màn hình sẽ xuất hiện toàn bộ câu lệnh hệ thống:
   - `help` : Hiển thị bảng danh sách các lệnh
   - `status` : Xem trạng thái an ninh, RAM, Tor daemon, Anti-Capture
   - `devtools` : Mở cửa sổ kiểm tra mã nguồn Chromium DevTools (F12)
   - `ram --flush` : Giải phóng bộ nhớ RAM và dọn sạch V8 Heap
   - `tor start` : Kích hoạt định tuyến Tor SOCKS5 (127.0.0.1:9050)
   - `tor stop` : Tắt mạng Tor, quay về mạng thông thường
   - `bypass-capture on` : TẮT chống chụp màn hình (Cho phép quay/chụp màn hình - GIẢM BẢO MẬT)
   - `bypass-capture off` : BẬT LẠI chống chụp màn hình (Bảo mật tối đa)
   - `flags` : Xem danh sách các cờ dòng lệnh Chromium đang chạy
   - `clear` : Xóa sạch màn hình dòng lệnh
   - `lock` : Khóa lại chế độ Developer Mode
   - `exit` : Trở về trang chủ `orbit://new-page`

| Phím tắt | Chức năng |
| :--- | :--- |
| `Ctrl + T` | Mở Tab thường mới |
| `Ctrl + Shift + N` | Mở Tab Ẩn danh (Yêu cầu Mật khẩu Chủ) |
| `Ctrl + W` | Đóng Tab hiện tại |
| `Ctrl + R` | Tải lại trang web |
| `Nhấn Esc 2 lần` | **🚨 Panic Wipe:** Hủy tức thì mọi tab ẩn danh và khóa an toàn |

---

## 📁 Cấu Trúc Các File & Thư Mục

```
OrBit/
├── Run-OrBit.bat                     <- File nhấp đúp để khởi chạy ngay
├── release/
│   └── OrBit-win32-x64/
│       ├── OrBit.exe                 <- File thực thi chính
│       ├── ffmpeg.dll                <- Thư viện giải mã Video/Audio HTML5
│       ├── d3dcompiler_47.dll        <- Thư viện tăng tốc đồ họa DirectX
│       ├── vk_swiftshader.dll        <- Thư viện đồ họa Vulkan
│       ├── vulkan-1.dll              <- Driver Vulkan
│       ├── libEGL.dll, libGLESv2.dll <- Bộ tăng tốc GPU
│       └── ...                       <- Toàn bộ tài nguyên Chromium gốc
├── src/
│   ├── security/
│   │   ├── vault.js                  <- Mã hóa AES-256-GCM + PBKDF2-SHA512
│   │   └── stealth.js                <- Cấu hình DoH, ECH, Anti-Capture, WebRTC
│   ├── performance/
│   │   └── optimizer.js              <- Hệ thống quản lý Sleeping Tabs & RAM
│   ├── browser/
│   │   └── tabs.js                   <- Quản lý đa tab WebContentsView
│   └── ui/
│       ├── index.html                <- Giao diện Chrome & Modal mật khẩu
│       ├── styles.css                <- Thiết kế giao diện
│       ├── renderer.js               <- Logic điều khiển UI
│       └── newtab.html               <- Trang New Tab bảo mật
└── main.js                           <- Điểm khởi đầu của ứng dụng
```
