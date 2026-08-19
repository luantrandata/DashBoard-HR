# KDI HR Analytics Dashboard

Dashboard phân tích nhân sự cho KDI Education. Single-file HTML, xử lý dữ liệu
hoàn toàn client-side (SheetJS + Chart.js được nhúng sẵn trong file — **không
cần internet, không có backend, không gửi dữ liệu lên server nào**).

## Cách dùng

1. Mở `index.html` (double-click hoặc host qua Cloudflare Pages — xem bên dưới).
2. Tải lên 2 file:
   - `KDI_Super_App_ThongTinNhanVien.xlsx`
   - `KDI_Super_App_ChamCongNhanVien.xlsx`
3. Bấm **Khởi tạo Dashboard**.

Dữ liệu chỉ tồn tại trong bộ nhớ trình duyệt của người dùng trong phiên đó —
tải lại trang là mất, cần upload lại. Đây là do thiết kế "không backend, không
lưu trữ" để tránh rủi ro bảo mật dữ liệu nhân sự.

## Cấu trúc

- `index.html` — toàn bộ dashboard (HTML + CSS + JS + 2 thư viện nhúng sẵn).
  Không có file phụ nào khác, không có build step.

## Deploy lên Cloudflare Pages qua GitHub

### Bước 1 — Đẩy code lên GitHub

```bash
cd kdi-hr-dashboard
git init
git add .
git commit -m "KDI HR Analytics Dashboard"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### Bước 2 — Kết nối Cloudflare Pages

1. Vào [dash.cloudflare.com](https://dash.cloudflare.com) → **Workers & Pages** → **Create application** → tab **Pages** → **Connect to Git**.
2. Chọn repo GitHub vừa tạo.
3. Ở màn hình **Build settings**:
   - **Framework preset**: `None`
   - **Build command**: để trống (không cần build)
   - **Build output directory**: `/` (dấu gạch chéo, KHÔNG gõ tên thư mục — đây là điểm hay bị nhầm)
4. Bấm **Save and Deploy**.

Sau vài chục giây, Cloudflare cấp cho bạn 1 URL dạng
`https://<project-name>.pages.dev` — mở link đó, upload 2 file Excel như hướng
dẫn ở trên là dùng được ngay.

### Cập nhật sau này

Mỗi lần bạn `git push` lên nhánh `main`, Cloudflare Pages tự động build & deploy
lại — không cần thao tác gì thêm trên dashboard Cloudflare.

## Lưu ý bảo mật / quyền riêng tư

File này **không có xác thực, không phân quyền** — bất kỳ ai có URL đều mở
được trang upload. Vì dữ liệu chỉ được xử lý cục bộ trên máy người dùng (không
gửi lên server) nên bản thân việc host file HTML không làm lộ dữ liệu nhân sự
— nhưng **URL Cloudflare Pages là public theo mặc định**. Nếu cần giới hạn
người truy cập, dùng tính năng **Cloudflare Access** (Zero Trust) để yêu cầu
đăng nhập email công ty trước khi vào trang.
