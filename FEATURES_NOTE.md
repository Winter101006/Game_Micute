# KawaiiCraft V5.2 — Giao Diện Không Chồng Chéo, Nhạc Dịu Êm & 3 Bản Đồ Hoàn Toàn Khác Biệt

Tác giả & Thiết kế: **Phạm Ngọc Huân** • Dành tặng riêng cho: **Bé Uyên 💖**

---

## 1. Các Nâng Cấp & Sửa Lỗi Chi Tiết Ở Phiên Bản V5.2

### 🧩 1. Hết 100% Lỗi Thanh Thông Báo & HUD Đè Lên Nhau (Flex Stack Architecture)
- **Khắc phục triệt để lỗi đè HUD ở bản V5.1:** Thay vì các thanh `fixed top-16`, `top-20`, `top-24`, `top-28` đè chồng lên nhau (như thanh `#minigame-hud-banner` che khuất `#battle-hp-hud`), toàn bộ 6 dải thông báo trên màn hình (`#toast`, `#map-invite-banner`, `#minigame-hud-banner`, `#battle-hp-hud`, `#partner-compass-indicator`, `#together-resonance-badge`) được gom vào chung 1 ngăn xếp dọc **`#hud-center-alerts-stack` (`flex-col`)**. Thanh nào hiện mới chiếm chỗ, cam kết **0px chồng chéo** trong mọi chế độ chơi!
- **Góc dưới-trái (`#bottom-left-hud-stack`):** Gom badge thú cưng `#pet-emote` xếp gọn ngay phía trên `#couple-chat-panel`, không đè lên khung chat.
- **Nhắc bấm tương tác (`#ride-action-prompt`):** Xếp ngăn nắp bên trên thanh Block Hotbar trong `#hud-bottom-bar`.

### 🔇 2. Mặc Định Tắt Nhạc Khi Mới Vào Game + Nhạc Lo-Fi Hộp Nhạc Dịu Êm
- **Yên tĩnh ngay khi mở game:** `KawaiiAudioEngine` khởi tạo với **`isMuted = true`**. Nút **`🔇 Tắt Nhạc`** đặt ngay ở hàng công cụ trên cùng để Huân & Uyên chủ động bật khi thích.
- **Nhạc nền êm ái kiểu hộp nhạc Ghibli / Lo-Fi:** Làm lại `startBGM()` với tiết tấu chậm rãi (`840–920ms`), hợp âm Maj7 nhẹ nhàng kết hợp bộ lọc trầm `lowpass 640Hz`, tiếng vang mượt không bị giật hay chói tai, kèm bass nền ấm áp. Âm lượng hiệu ứng (đặt/đập khối, nhảy, nhặt quà) cũng được làm dịu lại.

---

## 2. 3 Bản Đồ `320 x 320` Khác Biệt Hoàn Toàn & Trò Chơi Riêng Nhanh Gọn

| Bản Đồ | Địa Hình & Kiến Trúc Đặc Trưng | Đài Quan Sát | Minigame Riêng Trong Phím `U` |
| :--- | :--- | :--- | :--- |
| **1. 🏝️ Đảo Livik 4 Mùa** | Đảo 4 mùa quanh Hồ Trái Tim, Công Viên Giải Trí, Vòng Quay Siêu Cao **`Y=56`**, Mê Cung `44x44`, Đấu Trường `100 HP`. | **`Y = 54`** | Giữ nguyên toàn bộ **7 Khu Vui Chơi & Minigame Đôi** đầy đủ! |
| **2. ❄️ Vikendi Thung Lũng Tuyết** | **Bỏ hoàn toàn Vòng Quay & công trình giống Livik.** Thay bằng Thung Lũng Tuyết Bắc Cực, Dãy Núi Tuyết Hình Liềm, Pháo Đài Tuyết Đỉnh Bắc (`X:-48 Z:-82`), **Hồ Băng Cực Quang** & **Dốc Trượt Băng Thẳng `140m` xuyên 5 Cổng Cực Quang**. | **`Y = 48`** | **1. ⛄ Ném Tuyết Trúng Bia (30s):** Bắn 6 bia Người Tuyết (`Click/J/Q`).<br>**2. 🛷 Trượt Dốc Băng Thẳng (20s):** Giữ `W` trượt 1 mạch từ `Z:-94` xuống Hồ Băng! |
| **3. 🌴 Sanhok Quần Đảo 3 Đảo & Cầu Treo** | **Chia 3 hòn đảo tách biệt giữa biển ngọc** (Đảo Trung Tâm, Đảo Tây Hoàng Hôn, Đảo Đông Đền Cổ + Thác Nước, cộng Đảo Bắc Rừng Dừa) nối nhau bằng **3 Cây Cầu Treo Gỗ** bắc qua eo biển mở! | **`Y = 42`** | **1. 🥭 Nhặt Trái Vàng Trên Đảo (30s):** Chạy thu hoạch 10 Trái Vàng.<br>**2. 🌉 Đua Cầu Treo 3 Đảo (20s):** Chạy từ Đảo Tây (`X:-82`) qua 2 Cầu Treo tới Đảo Đông (`X:+72`)! |

- **Hub Minigame (`Phím U`) thông minh theo Map:** Tự động hiển thị bộ thẻ trò chơi tương ứng của Map đang đứng (`#hub-grid-livik`, `#hub-grid-vikendi`, `#hub-grid-sanhok`).
- **Radar & Minimap riêng biệt cho từng Map:** Radar cập nhật địa hình thật của từng thế giới (4 mùa Livik / Dốc băng thẳng + Hồ băng Vikendi / 3 đảo tách rời + 3 cầu treo Sanhok).
- **Đồng bộ mời đổi Map qua Firebase Realtime DB (`publicRooms` + `mapInvite`):** Đổi Map sẽ gửi lời mời sang cùng (`Phím Y`) và xác nhận đồng bộ 2 máy.

---

## 3. Phím Tắt Điều Khiển Nhanh (Zero-Interruption Flow)
- **`W / A / S / D`** + Chuột: Di chuyển & xoay góc nhìn • Bật nút **⚡ Chạy Nhanh** để chạy tốc độ cao liên tục.
- **`F` / `Space x2`:** Bật/Tắt Bay tự do — giữ **`Space`** hoặc nút **🦘 Nhảy** để bay lên mượt mà không giật rơi.
- **`U`:** Mở Hub Minigame theo từng Map • **`Chuột Trái / J / Q`:** Ném Tuyết / Cầu Tuyết Tim • **`K / Chuột Phải`:** Khiên Tim (`Battle 100 HP`).
- **`M`:** Mở Bản Đồ 3 Thế Giới & Click-to-Teleport • **`Y`:** Chấp nhận đổi Map cùng người yêu • **`G`:** Bay Tới Người Yêu • **`Tab`:** Ẩn/Hiện HUD.
