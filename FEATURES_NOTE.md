# KawaiiCraft V5.3 — Nhật Ký Nâng Cấp Toàn Diện Dữ Liệu, Kiến Trúc & Web Hướng Dẫn (`huong-dan.html`)

## 1. Tạo Mới Web Tài Liệu Tương Tác Giải Thích Chi Tiết (`huong-dan.html`)
- **Mục đích:** Cung cấp một trang web hướng dẫn kỹ thuật độc lập, trực quan bằng tiếng Việt giúp người dùng đọc hiểu rõ ràng từng thư mục, từng file trong `D:/Duan/Game_micute/`, cấu trúc dữ liệu đám mây và các công đoạn hoạt động.
- **6 Chuyên mục lớn bên trong `huong-dan.html`:**
  1. **🗂️ Bản Đồ Cây Thư Mục & Ý Nghĩa Từng File:** Giải thích chi tiết `.git/`, `.gitignore`, `index.html`, `huong-dan.html`, `kawaiicraft.html`, `README.md`, `FEATURES_NOTE.md`, và `vercel.json`.
  2. **☁️ Cấu Trúc Dữ Liệu Firebase Realtime Database & LocalStorage:** Sơ đồ nhánh `/publicRooms/{CODE}`, `/rooms/{CODE}/meta|players|blocks|events|minigames` và cơ chế lưu trữ vi sai `Delta Compression` (`kawaiicraft_v5_slot_1..3` + file `.kawaii`).
  3. **🧩 Giải Phẫu 12 Phân Hệ Trong `index.html`:** Chia nhỏ ~9.250 dòng code thành 12 phân hệ rõ ràng kèm tọa độ dòng và tên hàm chính.
  4. **⚙️ Giải Thích Chi Tiết 7 Công Đoạn Vận Hành:** Từ khởi tạo WebGL/Audio → Sinh 3 bản đồ `320×320` & `O(1) Surface Culling` → Vật lý bay mượt & HUD chống đè nhau → Ghép đôi Firebase `Zero Fake NPC` → Đồng bộ 11 Minigame → Auto-Save Delta → Git Push & Deploy Vercel.
  5. **🗺️ Từ Điển 3 Bản Đồ, 11 Trò Chơi & 36 Khối Voxel:** So sánh chi tiết Livik, Vikendi Tuyết và Sanhok Rừng.
  6. **🛠️ Cẩm Nang Tự Chỉnh Sửa Dữ Liệu Cho Anh Huân:** Hướng dẫn cụ thể từ khóa `Ctrl + F` để tự thêm lời chúc (`ROMANTIC_WISHES_POOL`), sửa phiếu quà (`REWARD_TYPES`), chỉnh nhạc (`KawaiiAudioEngine`) hoặc đổi cấu hình Firebase.

## 2. Nâng Cấp Đồng Bộ Toàn Bộ Hệ Thống Lên Phiên Bản V5.3
- **`index.html` (V5.3):**
  - Tích hợp nút mở nhanh **`📘 Web Giải Thích File`** trên thanh tiện ích mở rộng (`#extra-tools-drawer`) và bên trong Cẩm Nang Hướng Dẫn (`#help-modal`).
  - Nâng cấp toàn bộ dữ liệu `ROMANTIC_WISHES_POOL` và 5 Cột Mốc Cặp Đôi (`generate5MilestonesForMap`) khớp 100% với các trò chơi đặc sản mới của Vikendi và Sanhok.
- **`README.md` & `kawaiicraft.html` (V5.3):**
  - Cập nhật hoàn toàn tài liệu `README.md` từ bản V4.0 cũ lên chuẩn **V5.3** (Firebase Realtime Database, 3 Map `320×320`, 11 Minigame, 7 công đoạn kỹ thuật).
  - Nâng cấp `kawaiicraft.html` thành cổng chào V5.3 có nút vào thẳng Game (`index.html`) hoặc mở Web Giải Thích (`huong-dan.html`).

## 3. Các Cải Tiến Cốt Lõi Được Bảo Toàn Từ Bản V5.2
- **Chống đè các thanh thông báo (`#hud-center-alerts-stack`):** Mọi thanh thông báo (Toast, Điểm Minigame, Thanh máu 100 HP, Bảng mời đổi Map) tự động xếp hàng dọc không bao giờ che lấp nhau.
- **Mặc định tắt nhạc khi mới vào game (`🔇 Tắt Nhạc`):** Sử dụng bộ tổng hợp âm thanh Hộp Nhạc Lo-Fi (`triangle + sine` + `BiquadFilterNode 950Hz`) dịu êm khi người chơi bật lên.
- **3 Bản đồ khác biệt 100% (`resetWorldLandmarkGroups`):** Xóa sạch vòng quay và công trình của Livik khi chuyển sang Đảo Tuyết Vikendi hoặc Rừng Nhiệt Đới Sanhok.
