# KawaiiCraft V5.1 — Quần Đảo Đa Bản Đồ 320x320 & Khu Vui Chơi / 8 Minigame Cặp Đôi (Huân & Bé Uyên)

Tác giả & Thiết kế: **Phạm Ngọc Huân** • Dành tặng riêng cho: **Bé Uyên 💖**

---

## 1. Điểm Mới Nổi Bật Ở Phiên Bản V5.1 (Nâng Cấp Theo Trải Nghiệm Thực Tế)

### 🎡 Vòng Quay Siêu Cao (Đỉnh `Y = 56`) & Cabin Kính Thoáng 360°
- Nâng tâm vòng quay lên **`FERRIS_CENTER = (32, 34, -12)`** với bán kính **`R = 22` blocks** (đỉnh đạt **`Y = 56`**), giúp nhìn bao quát vượt qua toàn bộ lâu đài, cây anh đào và đảo mây.
- Thiết kế lại **8 Cabin Kính Toàn Cảnh**: bỏ tường chắn sau, thay bằng lan can kính thấp ngang thắt lưng và mái che nâng cao (`+1.15`), vị trí mắt ngồi ở `tmpRideVec.y - 0.15` cho tầm nhìn 360° không bị che khuất.

### 📡 Danh Sách Phòng Đang Mở (`publicRooms` — Vào Bằng 1 Chạm)
- Khi một người bấm **✨ Mở Phòng Ngay**, hệ thống tự động đăng phòng lên nhánh `/publicRooms/{ROOM_ID}` (kèm tên chủ phòng, bản đồ đang chơi, số người `1/2` và tự dọn sạch bằng `.onDisconnect().remove()`).
- Trong modal **💑 Chơi Chung**, Bé Uyên chỉ cần bấm nút **💞 Vào Luôn** ngay trên thẻ phòng đang mở mà không cần nhớ hay gõ lại mật khẩu/mã phòng!

### 🎨 Giao Diện HUD Chia Nhóm Khoa Học, Chat Gọn Góc Dưới Trái & Cụm Điều Khiển Góc Dưới Phải
- **Thanh công cụ trên cùng chia 3 nhóm rõ ràng:**
  - Nhóm **Điểm & Vị Trí** (trắng/hồng): Map badge tích hợp chuyển nhanh bản đồ, tọa độ khu vực, Tỉ số & Tim.
  - Nhóm **Hoạt Động Chính** (màu đậm nổi bật): Chơi Chung (tím-hồng), Khu Vui Chơi (cam-đỏ), Tới Người Yêu (hồng đậm), Bản Đồ (xanh dương), Cột Mốc Đôi (vàng) & Kho Quà.
  - Nhóm **Tiện Ích Phụ** (`⚙️ Thêm`): Thu gọn gọn gàng các nút ít dùng (Túi đồ, Ghép đồ, Mẫu nhà, Lưu, Đèn trời, Nhạc, Máy yếu, Hướng dẫn).
- **Khung Chat Tình Yêu** được đẩy sát góc **dưới-trái (`bottom-3 left-3`)** với nút **▼ Ẩn / ▲ Mở Chat** (hiển thị chấm hồng báo tin chưa đọc khi thu gọn).
- **Cụm nút nhanh góc dưới-phải (`#quick-action-pad`):** Bổ sung nút **☁️ Đài Mây (`Y=54`)**, nút **⚡ Chạy Nhanh** (bật/tắt chạy nhanh liên tục) và nút **⬆️ Nhảy / Giữ Bay Lên** dùng được trên cả PC lẫn cảm ứng.

### 🕊️ Sửa Triệt Để Lỗi Giật & Rơi Khi Giữ Phím `Space` Đang Bay
- Nguyên nhân gốc rễ: Giữ phím `Space` khoảng 2s kích hoạt sự kiện bàn phím lặp (`e.repeat === true`), liên tục rơi vào điều kiện nháy đúp `< 300ms` và bật/tắt `toggleFlyMode()` giữa không trung.
- Đã chặn hoàn toàn `if (!e.repeat)` trên phím `Space` nháy đúp và các phím chức năng khác — giữ `Space` hoặc nút **⬆️ Nhảy** bay lên cực kỳ mượt mà, ổn định!

---

## 2. 3 Thế Giới Rộng Lớn `320 x 320` Blocks & Đồng Bộ Đổi Map 2 Người (`Phím M`)

1. **🏝️ Map 1: Quần Đảo Livik 4 Mùa (`320x320`):**
   - 4 vùng sinh thái Xuân-Hạ-Thu-Đông rõ rệt quanh Hồ Trái Tim, Đỉnh Tuyết & Suối Nước Nóng, Máng Trượt Băng 2.5x, Thung Lũng Anh Đào, Rừng Phong, Bến Du Thuyền & Chú Vịt Vàng.
2. **❄️ Map 2: PUBG Vikendi Vương Quốc Tuyết (`320x320`):**
   - Phủ tuyết trắng & băng xanh toàn bản đồ: **Hồ Đóng Băng Trung Tâm**, **Lâu Đài Tuyết Vikendi** ở phía Bắc (`X:-12 Z:-85`), **Cảng Vũ Trụ Cosmodrome** (`X:65 Z:78`), **Tháp Radar Tuyết** & Rừng Thông Đóng Băng.
   - **Minigame độc quyền Vikendi:** 💎 **Săn 6 Tinh Thể Băng** rải khắp các công trình nổi bật của Vikendi!
3. **🌴 Map 3: PUBG Sanhok Rừng Rậm & Đền Cổ (`320x320`):**
   - Dòng **Sông Xanh uốn lượn hình chữ S** chia cắt rừng nhiệt đới với **3 Cây Cầu Treo Gỗ**, **Đền Cổ Đá Rong Ruins** (`X:-2 Z:-65`), **Trại Huấn Luyện Bootcamp** & Làng Nhà Sàn Bờ Sông.
   - **Minigame độc quyền Sanhok:** 🏛️ **Vượt Bẫy Đền Cổ** thu thập **5 Cổ Vật Vàng** trên khắp đảo rừng!
4. **Thông báo Mời Đổi Map Đồng Bộ + Radar Chỉ Đường Tương Tác:**
   - Khi 1 người chuyển bản đồ (bấm thanh trên cùng hoặc trong **Phím M**), người yêu lập tức nhận bảng mời nổi không ngắt chuột (`#map-invite-banner`) — bấm nút hoặc nhấn phím **`Y`** để sang cùng, sau đó cả 2 máy nhận thông báo xác nhận đã đồng bộ cùng một thế giới!
   - Radar góc trên phải và Bản đồ lớn (**Phím M**) tự cập nhật màu sắc địa hình, cầu/sông, vị trí 2 người theo từng Map; cho phép **Click trực tiếp lên Radar Bản Đồ Lớn** để dịch chuyển nhanh tới bất kỳ địa danh hay tọa độ nào!

---

## 3. Đài Ngắm Mây Toàn Cảnh (`Y=54`) & 8 Minigame Cặp Đôi (`Phím U`)

| STT | Trò Chơi / Khu Vui Chơi | Tọa Độ Trung Tâm | Cơ Chế & Luật Chơi |
| :-: | :--- | :--- | :--- |
| **1** | **🏃‍♂️ Đấu Trường Đuổi Bắt 50/50** (`36x36`) | `X:60 Y:5 Z:0` | Hiệp **45s**, tự đổi vai Huân ↔ Uyên. Người Đuổi `+6%` tốc độ (`<1.8m` bắt thắng). Người Chạy có **Lướt (`Shift`/`F`, hồi 7s)** + 4 Đệm Nhảy & 2 Cổng Dịch Chuyển. |
| **2** | **🌿 Mê Cung Tình Yêu** (`44x44`) | `X:-58.5 Y:6 Z:0.5` | Tường hoa cao 4 blocks + 3s đếm ngược + 3 Bình Tăng Tốc + nút đổi Seed đồng bộ Firebase. |
| **3** | **🎡 Vòng Quay Siêu Cao `Y=56`** | `X:32 Y:34 Z:-12` | 8 Cabin kính thoáng 360°, đỉnh đạt **`Y = 56`**, ngồi ngắm trọn đảo không bị che! |
| **4** | **🎠 Xích Đu Đôi Anh Đào** | `X:-34 Y:5 Z:-34` | Ngồi cạnh nhau dưới tán anh đào đung đưa nhẹ nhàng & thả tim. |
| **5** | **🎨 Sàn Nhảy Sắc Màu** (`6x6`) | `X:10 Y:5 Z:29` | Lưới 6 màu pastel trên hồ nước — hô màu 3s, rụng sàn 2s! |
| **6** | **🌈 Parkour & 🛷 Máng Trượt Băng** | `X:-14 Z:-26` → `Y:28` | Nhảy 3 Checkpoint lên Đảo Mây hoặc trượt đường băng tốc độ `2.5x`. |
| **7** | **⚔️ Đấu Trường Thanh Máu (`100 HP`)** | `X:50 Y:5 Z:40` | Đấu đối kháng thời gian thực với thanh **100 HP**: Ném Cầu Tuyết Tim (**`J` / `Q` / Chuột trái**, `-15 HP`), bật **Khiên Tim** (**`K` / Chuột phải**, giảm sát thương còn `-5 HP` trong 2.2s), nhặt **3 Bánh Kem Hồi `+20 HP`**. Hỗ trợ Bia Đấu Tập khi luyện 1 mình (tự xóa sạch khi kết thúc trận!). |
| **8** | **💎 / 🏛️ Đặc Sản Theo Map & ☁️ Đài Ngắm Mây** | Đài Mây: `X:0 Y:54 Z:-18` | **Săn 6 Tinh Thể Băng** ở Map Vikendi, **Vượt Bẫy Đền Cổ (5 Cổ Vật)** ở Map Sanhok, và **Đài Ngắm Mây Y=54** ngắm toàn cảnh 320x320. |

---

## 4. Phím Tắt Điều Khiển Nhanh (Zero-Interruption Flow)
- **`W / A / S / D`** + Chuột: Di chuyển & xoay góc nhìn (hoặc bật nút **⚡ Chạy Nhanh**)
- **`F` / `Space x2`:** Bật/Tắt Bay tự do — **giữ `Space` hoặc nút ⬆️ Nhảy** để bay lên mượt mà không giật rơi!
- **`U`:** Mở Hub **8 Minigame & Đấu Trường 100 HP** • **`J / Q / Chuột trái`:** Ném Cầu Tuyết Tim • **`K / Chuột phải`:** Khiên Tim
- **`M`:** Mở **Bản Đồ 3 Thế Giới & Radar Chỉ Đường Click-to-Teleport** • **`Y`:** Chấp nhận sang Map cùng người yêu
- **`E`:** Ngồi lên/xuống Vòng Quay `Y=56`, Xích Đu & đặt khối • **`G`:** Bay Tới Người Yêu • **`Tab`:** Thu gọn HUD
