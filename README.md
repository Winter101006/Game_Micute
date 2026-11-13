# 🌸 KawaiiCraft V5.3 — Thế Giới 3D Co-op 3 Bản Đồ (`320×320`) & 11 Minigame Dành Tặng Bé Uyên 💕

> **Phiên bản V5.3 (Couple Amusement Park, 3 Distinct Maps & Interactive Architecture Guide Edition)**
> Một thế giới Voxel 3D pastel lãng mạn chạy trực tiếp trên trình duyệt với tốc độ **60 FPS**, đồng bộ **2 người chơi thời gian thực qua Firebase Realtime Database** (`kawaii-craft-c7663`), sở hữu **3 bản đồ độc bản rộng `320 × 320`**, **11 trò chơi cặp đôi**, hệ thống **Hộp Nhạc Lo-Fi dịu êm (mặc định tắt khi mới vào)** và **Web Cẩm Nang Kiến Trúc Tương Tác (`huong-dan.html`)**.

---

## 🗂️ 1. Cấu Trúc Thư Mục & Ý Nghĩa Từng File Trong Dự Án (`D:/Duan/Game_micute/`)

```text
📁 D:/Duan/Game_micute/
├── 📁 .git/                # Cơ sở dữ liệu lịch sử Git & kết nối GitHub (huan2022004/Game-cua-uyen)
├── 📄 .gitignore           # Danh sách file rác hệ thống không đẩy lên GitHub (.DS_Store, Thumbs.db, *.log...)
├── 🎮 index.html           # [FILE CHÍNH ~9.250 DÒNG] Chứa toàn bộ Giao diện, Engine 3D Three.js, Âm thanh, 3 Map & Firebase Co-op
├── 📘 huong-dan.html       # [WEB HƯỚNG DẪN TƯƠNG TÁC] Trang web giải thích từng file, 12 phân hệ code & 7 công đoạn vận hành
├── 🚀 kawaiicraft.html     # [CỔNG KHỞI ĐỘNG NHANH] Trang Portal điều hướng vào thẳng Game (index.html) hoặc Web Hướng Dẫn
├── 📖 README.md            # [TÀI LIỆU MẶT TIỀN GITHUB] Hướng dẫn toàn diện dự án ở phiên bản V5.3
├── 📝 FEATURES_NOTE.md     # [NHẬT KÝ KỸ THUẬT] Ghi chép chi tiết các nâng cấp & bản vá từ V5.0 → V5.3
└── ⚡ vercel.json          # [CẤU HÌNH SERVER VERCEL] Thiết lập Clean URLs, Bảo mật Header & chống lưu Cache cũ
```

---

## 🌟 2. Các Điểm Nổi Bật Ở Phiên Bản V5.3

### 🗺️ A. 3 Bản Đồ `320 × 320` Khác Biệt Hoàn Toàn & Bộ Trò Chơi Đặc Sản Riêng
Khi chuyển Map bằng **Phím `M`** hoặc bấm vào **Radar góc trên phải**, hàm `resetWorldLandmarkGroups()` sẽ dọn sạch toàn bộ công trình của bản đồ cũ và kiến tạo thế giới mới hoàn toàn:

| Bản Đồ (`320×320`) | Địa Hình & Công Trình Đặc Trưng | Các Trò Chơi Đặc Sản (Mở bằng Phím `U`) |
| :--- | :--- | :--- |
| **1. 🌸 Đảo Livik 4 Mùa** (`livik_island`) | 4 vùng khí hậu (Xuân Anh Đào, Biển Hè, Rừng Thu, Đỉnh Tuyết), Vòng Quay Mặt Trời siêu cao `Y=56` (cabin mở 360° không bị che), Lâu Đài Mây. | • **⚔️ Đấu Trường Thanh Máu 100 HP**<br>• **🎡 Vòng Quay Mặt Trời Y=56**<br>• **🏃‍♂️ Đuổi Bắt Tình Yêu 60s**<br>• **🧩 Đua Mê Cung Trái Tim**<br>• **🎠 Xích Đu Đôi**, **🕺 Sàn Nhảy Disco**, **🌈 Parkour Cầu Vồng** |
| **2. ❄️ Đảo Tuyết Vikendi** (`vikendi_snow`) | **Không có vòng quay Livik.** Toàn đảo phủ băng tuyết pha lê, Hồ Băng Trung Tâm, Lâu Đài Băng Hoàng Gia, Làng Lều Tuyết Igloo & Đường Đua Trượt Tuyết. | • **🛷 Đua Trượt Băng Cặp Đôi (`vikendiRace`)**: Lướt băng siêu tốc qua 5 Cờ Tuyết.<br>• **⛄ Đại Chiến Cầu Tuyết 100 HP (`hpBattle`)**<br>• **⭕ Cờ Caro Băng Giá 3×3 (`tictactoe`)** |
| **3. 🌴 Rừng Nhiệt Đới Sanhok** (`sanhok_jungle`) | **Không có vòng quay Livik.** Rừng nhiệt đới xanh thẫm chia cắt bởi sông Ngọc Lục Bảo, Đền Tháp Cổ Maya (`Bootcamp`), Bến Thuyền Paradise & Nhà Sàn. | • **🔥 Nhảy Bục Né Nước Nóng (`sanhokZone`)**: Nhảy qua 16 bục đá cổ nhặt Ngọc Rừng Xanh.<br>• **💓 Thi Bấm Tim Tốc Độ 10s (`heartTap`)**<br>• **🏹 Đấu Trường Rừng Xanh 100 HP (`hpBattle`)** |

### 🛡️ B. Hệ Thống Thanh Thông Báo Chống Đè Nhau (`Zero-Overlap HUD Stack`)
- Toàn bộ các bảng thông báo ở giữa màn hình (Thông báo hoàn thành cột mốc, Thanh điểm Minigame, Thanh máu đối kháng 100 HP, Bảng mời đổi Map cùng người yêu) đều được đặt chung trong container dọc `#hud-center-alerts-stack` (`flex-col gap-1.5`).
- Khi nhiều bảng cùng xuất hiện, chúng **tự động xếp chồng xuống dưới gọn gàng**, tuyệt đối không bao giờ đè chữ lên nhau.

### 🎵 C. Hộp Nhạc Lo-Fi Dịu Êm & Mặc Định Tắt Khi Mới Vào Game
- Khi mới mở game, âm nhạc **mặc định ở trạng thái TẮT (`🔇 Tắt Nhạc`)** để không gây giật mình.
- Khi người chơi bấm nút bật nhạc trên thanh công cụ, `KawaiiAudioEngine` tạo giai điệu Hộp Nhạc Lo-Fi (`Fmaj7 – Cmaj7 – Dm7 – G7`) bằng sóng âm `triangle + sine` lọc qua `BiquadFilterNode (950Hz)` vô cùng êm dịu.

### 💑 D. Chơi Chung 2 Người Qua Firebase Realtime Database (`Zero Fake NPC`)
- **Không có NPC giả:** Khi chơi 1 mình, trên bản đồ hoàn toàn không có nhân vật thứ 2 đứng đơ. Chỉ khi người yêu thực sự kết nối vào nhánh `/rooms/{ROOM_ID}/players`, mô hình 3D của đối phương mới xuất hiện.
- **Danh Sách Phòng Đang Mở (1 Chạm Vào Luôn):** Khi Anh Huân tạo phòng, tên phòng tự động hiện lên mục **📡 Danh Sách Phòng Đang Mở** (`/publicRooms`) để Bé Uyên bấm 1 chạm vào thẳng phòng mà không cần gõ mật khẩu.
- **Đồng Bộ Đổi Map Chung (`Phím Y`):** Khi 1 người chuyển sang bản đồ khác, người kia nhận được thông báo mời và chỉ cần bấm phím `Y` để bay sang cùng bản đồ ngay lập tức.

---

## ⚙️ 3. Tóm Tắt 7 Công Đoạn Vận Hành Của Hệ Thống

1. **Công đoạn 1 — Khởi tạo & Vẽ vật liệu tự động:** Nạp `Three.js r128`, khởi tạo `KawaiiAudioEngine` ở chế độ tắt nhạc mặc định, và dùng `<canvas>` vẽ 36 chất liệu khối Voxel trong RAM.
2. **Công đoạn 2 — Sinh bản đồ `320×320` & Tối ưu `InstancedMesh`:** Dọn sạch công trình cũ bằng `resetWorldLandmarkGroups()`, sinh địa hình mới và dùng `isBlockExposed()` ẩn các khối bị che khuất để giữ 60 FPS.
3. **Công đoạn 3 — Vật lý 60 FPS & Điều khiển bay mượt:** Xử lý va chạm AABB, lọc bỏ sự kiện lặp phím (`e.repeat`) để giữ phím `Space` bay vút lên cao không bao giờ bị giật hay rơi xuống.
4. **Công đoạn 4 — Ghép đôi Firebase & Danh sách phòng `publicRooms`:** Đồng bộ vị trí `x, y, z, yaw, pitch` ở tần số 15Hz kết hợp nội suy `Lerp` 60 FPS, tự động xóa nhân vật khi đóng tab (`onDisconnect().remove()`).
5. **Công đoạn 5 — Vận hành 11 Minigame & Đấu Trường 100 HP:** Đồng bộ điểm số, thanh máu 100 HP, đường đạn cầu tuyết/pháo tim, bánh kem hồi `+20 HP`, cờ Caro 3×3 và lời mời đổi Map qua nhánh `/rooms/{ROOM_ID}/minigames`.
6. **Công đoạn 6 — Lưu trữ vi sai (`Delta Compression`):** Tự động lưu các khối xây thêm (`added`), khối đập đi (`removed`), 5 cột mốc và Kho Phiếu Quà vào 3 Slot `localStorage` hoặc xuất ra file `.kawaii`.
7. **Công đoạn 7 — Triển khai GitHub & Vercel Cloud:** Đẩy code lên nhánh `main` của GitHub (`git push origin main`), máy chủ Vercel đọc `vercel.json` và tự động xuất bản phiên bản mới sau ~15 giây.

> 💡 **Xem bản giải thích trực quan đầy đủ nhất:** Hãy mở file **[huong-dan.html](huong-dan.html)** trên trình duyệt (hoặc bấm nút **`📘 Web Giải Thích File`** ngay trong game)!

---

## 🎮 4. Bảng Phím Tắt Điều Khiển Nhanh

| Phím / Thao tác | Chức năng |
| :--- | :--- |
| **`W, A, S, D`** | Di chuyển nhân vật |
| **`Space`** (Bấm 1 lần) / Nút **`⬆️ Nhảy`** | Nhảy lên (hoặc giữ chặt `Space` để bay lên cao khi đang ở chế độ Bay) |
| **`Shift`** / Nút **`⚡ Chạy Nhanh`** | Tăng tốc chạy nhanh |
| **`Phím F`** (hoặc nháy đúp `Space`) | Bật / Tắt chế độ Bay tự do |
| **`Phím E`** / Chuột phải | Đặt khối xây dựng / Ngồi lên Vòng Quay hoặc Xích Đu |
| **`Chuột trái` / `Phím Q` / `Phím J`** | Đập khối / Bắn cầu tuyết hoặc pháo tim trong Đấu Trường 100 HP |
| **`Phím K`** | Bật Khiên Trái Tim giảm 50% sát thương (trong Đấu Trường) / Tặng Hoa |
| **`Phím U`** | Mở Trung Tâm Khu Vui Chơi & 11 Minigame theo từng Map |
| **`Phím M`** | Mở Bản Đồ Hướng Dẫn `320×320`, Dịch chuyển nhanh & Đổi giữa 3 Map |
| **`Phím G`** | Bay tức thì tới cạnh người yêu (khi đang chơi Co-op) |
| **`Phím Y`** | Đồng ý đi theo người yêu sang Bản đồ mới |
| **`Phím T` / `Phím V` / `Phím P`** | Thả mưa tim 💖 / Múa vẫy tay 💃 / Chụp ảnh Selfie Đôi Polaroid 📸 |
| **`Phím Tab`** | Ẩn / Hiện giao diện HUD để ngắm cảnh toàn màn hình |
