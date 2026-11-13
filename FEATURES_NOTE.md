# KawaiiCraft V5.5 — Đồ Họa 4 Mức Tăng Dần (Mức 3 = V5.3, Mức 4 = Cực Phẩm), Texture 64×64 Nét Căng & Va Chạm AABB Chuẩn

## 1. Sửa Triệt Để Lỗi Đi Xuyên Khối (`collidesPlayerAABB` & Sub-Stepping)
- Thay thế kiểm tra 1 điểm đơn giản bằng **Hộp Va Chạm 3D AABB (`PLAYER_RADIUS = 0.28`, `PLAYER_HEAD_CLEAR = 0.16`, `player.height = 1.6`)** kiểm tra đồng đều từ bàn chân tới đỉnh đầu.
- Áp dụng va chạm chuẩn trên cả **Đi Bộ**, **Chạy Nhanh / Trượt Băng (`subSteps <= 0.16m`)**, **Nhảy Đụng Trần (`ceilBlockBottom`)** và **Bay Tự Do (`player.isFlying`)** — không còn đi hoặc bay xuyên tường, nhà, cây hay cầu đá!
- Tự động tách trục X/Z mượt dọc tường (`wall sliding`), hỗ trợ leo bậc cao 1 khối hợp lệ khi thoáng đầu, bơi nhẹ nhàng qua Nước (`id: 7`) và lướt qua Hoa/Lúa nhỏ (`id: 30, 33`). Chặn đặt khối mới đè vào thân người chơi (`doesBlockOverlapPlayer`).

## 2. Nâng Cấp Đồ Họa Sắc Nét & Chia 4 Mức Tăng Dần (`GRAPHICS_LEVELS 1 → 4`)
- **Texture 64×64 sắc nét & Khử răng cưa (`antialias: true`):** Vẽ lại toàn bộ texture thủ công `64×64` có viền bevel 3 mặt rõ rệt, họa tiết gạch/cỏ/gỗ/nước/pha lê chi tiết kết hợp lọc `NearestFilter + anisotropy` và tầm nhìn `camera.far = 1000`.
- **4 Mức Đồ Họa chọn trực tiếp trong bảng `🎨 Đồ họa` (`#perf-modal`), tự lưu vào `localStorage`:**
  1. **Mức 1 — Siêu Nhẹ (`0.9x`, Fog `215m`, Lambert):** Tắt hạt, sinh vật, bóng, mây & cầu vồng để đạt FPS cao nhất trên máy yếu.
  2. **Mức 2 — Nhẹ Mượt (`1.0x`, Fog `300m`, Lambert):** Bật đầy đủ sinh vật, cầu vồng và hạt môi trường tiết kiệm (`max 16`).
  3. **Mức 3 — Chuẩn Đẹp V5.3 ⭐ (Mặc Định — `1.25x`, Fog `380m`, PBR `MeshStandardMaterial` `roughness 0.50`):** Giữ đúng chất đồ họa sắc nét, sáng mịn và thông thoáng nguyên bản của bản V5.3.
  4. **Mức 4 — Cực Phẩm Sáng Tạo ✨ (`2.0x Ultra HD`, Fog `560m`, `ACESFilmicToneMapping`):** Kích hoạt **Bóng đổ nắng thật (`PCFSoftShadowMap` bám theo người chơi)**, **Tầng Mây Kẹo Bông 3D bay trôi + Đĩa Mặt Trời / Vầng Trăng & Sao đêm**, **Ánh sáng vòm trời 3 chiều (`HemisphereLight`)**, **Pha lê / Nước / Băng bóng phản chiếu & nước gợn sáng**, cùng hiệu ứng hạt dày gấp đôi.

---

# KawaiiCraft V5.4 — Tối Ưu Siêu Nhẹ 60 FPS, Bảng Độ Nặng & HUD Góc Gọn

## 1. Dời Toàn Bộ Thanh Trạng Thái Vào Góc Trái Gọn Gàng (`#hud-center-alerts-stack`)
- Chuyển cụm `#hud-center-alerts-stack` (`#minigame-hud-banner`, `#battle-hp-hud`, `#toast`, `#map-invite-banner`, `#partner-compass-indicator`, `#together-resonance-badge`) từ giữa màn hình sang **góc trên bên trái (`top-[78px] left-2.5 w-[228px] sm:w-[258px]`)**.
- Bổ sung nút thu gọn/mở rộng (`▼ Thu gọn`) ngay trên banner minigame để người chơi có tầm nhìn rộng thoáng tối đa giữa màn hình.

## 2. Tinh Giảm Độ Nặng & Triệt Tiêu Khựng Lag (Anti-Lag V5.4)
- **Xóa sạch GPU `backdrop-filter: blur(...)`** khỏi `.cozy-glass`, thanh HUD trên và tất cả các bảng chọn (`#minigames-modal`, `#perf-modal`, v.v.) giúp mở bảng chọn trò chơi mượt tức thì.
- **Tạm giảm tải 3D khi mở bảng (`isAnyFullscreenModalOpen()`):** Giới hạn render 3D phía sau xuống 1/4 tần suất và tạm dừng quét sinh vật/hạt/minimap để CPU/GPU dồn 100% cho giao diện chọn trò chơi.
- **Chống khựng khi di chuyển (`Delta-Time` + `Zero-GC`):** Loại bỏ khởi tạo `THREE.Vector3`/`Euler` mới mỗi khung hình trong `raycastVoxel()` và `updatePlayerMovement(dtScale)`, bổ sung cache text chống ghi DOM trùng lặp (`_lastCoordsStr`, `_lastRadarPartnerKey`, `_lastMgHudKey`).
- **Tái sử dụng hạt (`particlePool`) & Shader `MeshLambertMaterial`:** Thay `MeshStandardMaterial` PBR nặng bằng `MeshLambertMaterial` nhẹ (~2–3× nhanh hơn), giảm mặc định `antialias: false`, `pixelRatioCap: 1.0`, `fogFar: 290`, ẩn luôn mesh loại khối có `count === 0`.
- **Chống khựng định kỳ mỗi 10 giây (`isWorldSaveDirty`):** Chỉ ghi `localStorage` khi có thay đổi (`force = false` cho Auto-Save nền) và không dựng lại HTML thẻ slot nếu `#save-modal` đang đóng.

## 3. Bảng Soi Độ Nặng & Tinh Chỉnh Mượt Thời Gian Thực (`#perf-modal`)
- Bấm thẳng vào nút **`60 FPS 📊 Độ nặng`** trên thanh góc trên hoặc vào **`⚙️ Thêm ▾ -> 📊 Độ Nặng / Mượt`** để xem:
  - Điểm FPS / ms khung hình (`renderMs` GPU), số Voxel đang vẽ vs ẩn (`Surface Culling`), số Draw Calls, và tỷ lệ % độ nặng của 5 phân hệ (Địa hình Voxel, GPU Fill-Rate & Fog, Sinh vật & Công trình động, Hạt Particle Pool, HUD & Bản đồ con).
  - Top 5 loại khối nặng nhất trên bản đồ hiện tại.
  - 3 nút cấu hình nhanh **🚀 Siêu Nhẹ**, **⚖️ Cân Bằng**, **✨ Nét Cao** cùng 4 nút bật/tắt chi tiết từng phần.

---

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
