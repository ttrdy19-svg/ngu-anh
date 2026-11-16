# Ngư Ảnh

Trình duyệt không giao diện (headless) nhẹ, viết bằng Rust + V8, nói giao thức Chrome DevTools (CDP) — chạy được
Playwright / Puppeteer như Chrome headless nhưng tốn ít RAM hơn nhiều. Dùng trong dây chuyền làm MV của Duy TTD Studio
để mở nhiều phiên web cùng lúc trên một máy nhà.

Ngư Ảnh là **bản sửa đổi của [Obscura](https://github.com/h4ckf0r0day/obscura)** (Apache License 2.0). Giấy phép gốc giữ nguyên
ở `LICENSE`; danh sách thay đổi ở `NOTICE`; README gốc ở `README-OBSCURA.md`.

## Ngư Ảnh thêm gì so với Obscura

- WebSocket thật (tokio-tungstenite + rustls) — bản gốc là giả lập, các trang chat không nhận được tin.
- `importScripts()` trong Worker (tải đồng bộ), `DataTransfer` + gán `input.files` (tải file lên), gõ `contenteditable`
  (`insertText` / `execCommand`), `contentEditable`.
- `blob:` giữ đúng byte, `fetch(blob:)`, `<img src=blob:>`; `MessagePort` xuyên khung (reCAPTCHA); `canPlayType` như Chrome.
- `Runtime.evaluate` với `awaitPromise` không bị cắt ở 30 s / 60 s; ghi vết lỗi Worker.

## Dựng

```bash
cargo build --release -p obscura-cli --bins --features render
```

Tên file chạy hiện vẫn là `obscura` / `obscura-worker` (đổi dần). Cách chạy và giao thức: xem `README-OBSCURA.md` và `docs/`.

## Giấy phép

Apache License 2.0 (giữ như bản gốc). "Obscura" là tên của dự án gốc; Ngư Ảnh không phải sản phẩm chính thức của họ.
