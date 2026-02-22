# 🔒 SecretLink

Chat P2P bí mật. Chỉ cần 1 repo GitHub + GitHub Pages. Không cần server riêng.

---

## Cấu trúc thư mục

```
secretlink/
├── index.html          ← Toàn bộ ứng dụng
└── lang/
    ├── manifest.json   ← Danh sách ngôn ngữ
    ├── vi.json         ← Tiếng Việt
    ├── en.json         ← English
    └── fr.json         ← (ví dụ thêm tiếng Pháp)
```

---

## Deploy lên GitHub Pages

1. Push tất cả file lên repo GitHub
2. Vào **Settings → Pages → Source: Deploy from branch → main / root → Save**
3. Truy cập: `https://username.github.io/secretlink/`

---

## Cách dùng

| Người A | Người B |
|---------|---------|
| Bấm **"+ Tạo phòng mới"** | Nhập mã 6 ký tự |
| Gửi mã phòng (hoặc link) cho B | Bấm **"Vào phòng →"** |
| ✅ Kết nối P2P tự động | ✅ Kết nối P2P tự động |

---

## Thêm ngôn ngữ mới

### Bước 1 — Tạo file ngôn ngữ

Tạo `lang/fr.json` (ví dụ tiếng Pháp), sao chép nội dung từ `vi.json` và dịch tất cả giá trị:

```json
{
  "meta": {
    "code": "fr",
    "name": "Français"
  },
  "ui": {
    "status_idle": "Non connecté",
    "create_room": "+ Créer une salle",
    ...
  }
}
```

### Bước 2 — Khai báo trong manifest

Mở `lang/manifest.json` và thêm mã ngôn ngữ:

```json
["vi", "en", "fr"]
```

### Bước 3 — Push lên GitHub

App sẽ tự động phát hiện ngôn ngữ mới và thêm vào dropdown khi người dùng tải trang.

---

## Tính năng

| Tính năng | Chi tiết |
|-----------|----------|
| 💬 Chat text | Real-time qua WebRTC DataChannel |
| 📎 Gửi file | Tối đa 20MB, nút ngang hàng ô chat, drag & drop |
| 🗑 Xoá hội thoại | Nút xoá trong header, có xác nhận |
| ⚠ Cảnh báo mất focus | Thông báo người kia khi bạn rời tab (không tự ngắt) |
| 💓 Heartbeat | Ping/pong 10 giây, phát hiện mất kết nối |
| ⏱ Inactivity | Không chat 5 phút → đếm ngược 30 giây rồi ngắt |
| 🌐 i18n | Tách file ngôn ngữ riêng, tự động phát hiện ngôn ngữ mới |

---

## Lưu ý kỹ thuật

- **Signaling** qua PeerJS public server (`peerjs.com`) — miễn phí, không cần cấu hình
- Sau khi WebRTC kết nối, **mọi dữ liệu đi P2P** — không qua server nào
- Không lưu bất kỳ dữ liệu nào (localStorage, cookie, database)
- File ngôn ngữ (`lang/*.json`) được tải qua `fetch()` → cần HTTPS (GitHub Pages ✅)
- Nếu mở `file://` local sẽ dùng fallback tiếng Việt nội tuyến tự động
