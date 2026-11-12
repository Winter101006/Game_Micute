# KawaiiCraft V5.0 — Đảo Livik 320x320 & Khu Vui Chơi / 6 Minigame Cặp Đôi (Huân & Bé Uyên)

Tác giả & Thiết kế: **Phạm Ngọc Huân** • Dành tặng riêng cho: **Bé Uyên 💖**

---

## 1. Trải nghiệm Liền Mạch (Zero-Interruption Flow)
- **Loại bỏ hoàn toàn Popup/Modal ngắt quãng:** Hoàn thành Cột Mốc hay mở Hộp Quà Bí Mật không còn tự động bật bảng làm mất chuột (`exitPointerLock`).
- **Thông báo Toast Banner 3 giây:** Trượt nhẹ nhàng ở cạnh trên màn hình (`pointer-events-none`) kèm âm thanh *ting!* dịu nhẹ.
- **Rút gọn còn 5 Cột Mốc Cặp Đôi Lớn (`Phím N`):**
  1. Chơi 1 ván **Đấu Trường Đuổi Bắt Cân Bằng 50/50** cùng nhau.
  2. Đua **Mê Cung Tình Yêu 44x44** & chạm **Cúp Trái Tim Vàng** ở tâm mê cung.
  3. Ngồi chung **Cabin #0 Vòng Quay Mặt Trời Khổng Lồ** ngắm toàn cảnh đảo Livik.
  4. Chinh phục **Đỉnh Tuyết Livik & Suối Nước Nóng** (hoặc Đỉnh Taiga trong Map Minecraft).
  5. Cùng nhau đặt **15 khối** xây tổ ấm chung của hai đứa.

---

## 2. Thế Giới Mở Rộng Gấp 4 Lần (`320 x 320` Blocks) & Tối Ưu 60 FPS
- **Kích thước thế giới:** `WORLD_RADIUS = 160` (`X: -160..160`, `Z: -160..160`, tổng diện tích `320 x 320` blocks) cho cả **Đảo Livik 4 Mùa** và **Lục Địa Minecraft Cổ Điển**.
- **Các khu vực nổi bật mới:**
  - **Bắc & Đông Bắc:** Đỉnh Núi Tuyết hùng vĩ (`Y ~ 16-22`), Suối Nước Nóng bốc khói (`X:75 Z:-91`), **Máng Trượt Băng Tốc Độ 2.5x** (`X:84 Y:17 Z:-70` trượt xuống `X:50 Y:5 Z:-28`).
  - **Tây Bắc:** Thung Lũng Hoa Anh Đào mở rộng, **Cối Xay Gió Khổng Lồ** (`X:-88 Z:-78`) & **Xích Đu Đôi Anh Đào**.
  - **Trung Tâm:** Hồ Trái Tim, Thác Nước Pha Lê, **Công Viên Giải Trí Đôi** & **Lâu Đài Mây trên không (`Y = 28`)**.
  - **Tây Nam & Đông Nam:** Rừng Phong Lá Đỏ, Vườn Bí Ngô & Nhà Kho Đỏ (`X:-75 Z:75`); Vịnh Nắng Hạ, Bến Du Thuyền dài (`X:92 Z:78..126`), Du Thuyền Pastel (`X:100 Z:122`), Chú Vịt Vàng Khổng Lồ (`X:108 Z:102`) & Các Đảo Nhỏ Ngoài Khơi.
- **Tối ưu hiệu năng 60 FPS:**
  - `THREE.InstancedMesh` với `frustumCulled = false` + giới hạn buffer thông minh theo loại khối.
  - **Surface Culling & Spatial Hash `Uint8Array` (`staticColliderGrid`):** Kiểm tra va chạm và occlusion ở độ phức tạp $O(1)$, không gây giật lag khi sinh bản đồ `320 x 320`.
  - **Fast Delta Save (`V5.0`):** `localStorage` chỉ lưu mảng `worldDeltas` các khối người chơi tự đặt/đập (< 1ms mỗi lần lưu tự động).
  - **Particle Camera Culling:** Hạt thời tiết (tuyết, hoa đào, lá phong, nắng) chỉ sinh trong bán kính `<= 20 blocks` quanh `camera` và tái sử dụng material.

---

## 3. Khu Vui Chơi & 6 Minigame Đồng Bộ Firebase (`Phím U`)

Tất cả minigame và bảng tỉ số (`🏆 Huân X - Y Uyên`) được đồng bộ thời gian thực qua **Firebase Realtime Database (`kawaii-craft-c7663`)** tại nhánh `/rooms/{ROOM_ID}/minigames`.

| STT | Trò Chơi / Khu Vui Chơi | Tọa Độ Trung Tâm | Cơ Chế & Luật Chơi |
| :-: | :--- | :--- | :--- |
| **1** | **🏃‍♂️ Đấu Trường Đuổi Bắt 50/50** (`36x36`) | `X:60 Y:5 Z:0` | Hiệp **45 giây**, tự đóng cổng sân, tắt Bay & khóa đập khối. **Người Đuổi** có hào quang Đỏ-Cam + **+6% tốc độ** (`< 1.8m` là bắt thắng). **Người Chạy** có hào quang Xanh Mint + kỹ năng **Lướt Nhanh (`Shift` / `F`, hồi 7s)**. Sân đối xứng có **4 Đệm Nhảy Lò Xo (Khối `38`)** & **2 Cổng Dịch Chuyển (`X:60 Z:-15` ↔ `X:60 Z:14`, Khối `39`)**. Tự đổi vai mỗi hiệp! |
| **2** | **🌿 Mê Cung Tình Yêu** (`44x44`) | Cổng `X:-59 Z:23`<br>Tâm `X:-58.5 Z:0.5` | Tường cây cao 4 blocks không thể nhìn xuyên. Đếm ngược 3s trước khi mở Cổng Xuất Phát. Có **3 Bình Tăng Tốc (+55% trong 5s)** ở các ngõ rẽ & **Nút Đổi Sơ Đồ** (seed đồng bộ Firebase giữa 2 máy). Chạm **Cúp Trái Tim Vàng** trước để thắng! |
| **3** | **🎡 Vòng Quay Mặt Trời Khổng Lồ** | `X:28.5 Y:20 Z:-8` | Cao `28 blocks` với 6 Cabin Pastel luôn cân bằng thẳng đứng khi vòng quay xoay liên tục. Đứng gần bấm **`E`** (hoặc từ Hub `U`) để Huân & Uyên ngồi chung **Cabin #0** ngắm toàn cảnh đảo `320x320`. Bấm **`E`** hoặc **`Space`** để xuống. |
| **4** | **🎠 Xích Đu Đôi Anh Đào** | `X:-34 Y:5 Z:-34` | Dưới gốc Hoa Anh Đào cổ thụ. Bấm **`E`** để ngồi cạnh nhau đung đưa nhịp nhàng theo sóng `Math.sin` và tỏa bong bóng trái tim hồng. |
| **5** | **🎨 Sàn Nhảy Sắc Màu** (`6x6`) | `X:10 Y:5 Z:29` | Lưới `6x6` ô (`3x3` block/ô) gồm 6 màu pastel (`🍓 Hồng Dâu`, `🍊 Cam Đảo`, `🍋 Vàng Chanh`, `🍏 Bạc Hà`, `🫐 Xanh Ngọc`, `🍇 Khoai Môn`) nổi trên hồ nước. Cứ mỗi lượt, hệ thống hô màu **3 giây** để chạy tới ô đúng trước khi các màu khác biến mất **2 giây**! Ai rơi xuống hồ nước bị loại. |
| **6** | **🌈 Parkour Cầu Vồng & 🛷 Máng Trượt Băng** | Parkour: `X:-14 Z:-26` → `Y:28`<br>Trượt Băng: `X:84 Y:17 Z:-70` | **Parkour:** Nhảy bậc cầu vồng qua **3 Checkpoint** lên thẳng Đảo Mây (`Y=28`) tính giờ không dùng Bay.<br>**Máng Trượt Băng:** Đường băng tuyết từ Đỉnh Núi Tuyết xuống trung tâm công viên — tự động kích hoạt tốc độ **lướt `2.5x`** trên Khối Băng (`ID 8`)! |

---

## 4. Phím Tắt Điều Khiển Chính
- **`W / A / S / D`** + Chuột: Di chuyển & xoay góc nhìn
- **`Shift` / `F` (trong Đuổi Bắt):** Kỹ năng **Lướt Nhanh** cho Người Chạy (hồi `7s`)
- **`F` / `Space x2` (ngoài Minigame):** Bật/Tắt chế độ Bay tự do
- **`U`:** Mở Hub **Công Viên Giải Trí & 6 Minigame Cặp Đôi**
- **`E` (gần Vòng Quay / Xích Đu):** Ngồi lên / Xuống khỏi trò chơi đôi
- **`E` / Chuột Phải:** Đặt khối hoặc mở Tương tác (Hộp Nhạc, Pháo Hoa, Biển Chữ, Hộp Quà)
- **`Q` / Chuột Trái:** Đập khối
- **`N`:** Mở bảng **5 Cột Mốc Cặp Đôi** | **`M`:** Bản Đồ Di Chuyển | **`G`:** Bay Tới Người Ấy (khi Co-op) hoặc Mẫu Nhà
- **`T / V / K / P`:** Thả Tim / Nhảy Vui / Tặng Hoa / Chụp Ảnh Selfie hoặc Gọi Thú Cưng
- **`Tab`:** Thu gọn HUD tối đa để ngắm cảnh toàn màn hình
