# HANT – KPI Workspace (mobile champagne edition)

Phiên bản chính trên nhánh `main` đã được thay bằng giao diện mobile vàng champagne, **sử dụng engine tính KPI và cơ chế đồng bộ từ `tohanh1/hanh-kpi`**.

## Giao diện trên điện thoại
- Thu tiền: từng khoản thu là một thẻ thu gọn; chạm để mở và sửa thông tin.
- NTU: Tiền thu vẫn hiển thị; Mindue, POS đã thu (tự điền) và Hệ số trách nhiệm nằm trong phần mở rộng.
- Dùng `touch-action: manipulation` để hạn chế zoom khi chạm hai lần lên giao diện, nhưng giữ nguyên pinch-to-zoom vì lý do hỗ trợ tiếp cận.
- Bảng màu chính: vàng champagne `#C99A25`, trắng ngà `#F7F7F5`.

## Nghiệp vụ
- Giữ nguyên hàm `calc(s)`, `posOf`, `fixPe`, `fixPos`, các bảng hệ số và cơ chế tạo/ghép thay đổi đồng bộ.
- `Code.gs` được sao chép không chỉnh sửa từ `hanh-kpi/main`, **chỉ để tham chiếu và triển khai khi người dùng tự chọn**. Nó không tự kết nối Sheet thật.
- Target NTU (`tNTU`), NTU CIC OK (`ntuOK`) và số hồ sơ đạt mindue được giữ tách biệt theo nghiệp vụ gốc.
- `sw.js` chỉ cache tài nguyên tĩnh trong cùng origin, bỏ qua URL có query string.
- Bao gồm `manifest.webmanifest`, `icon.svg` cho PWA.

## Lưu trữ, sao lưu và khôi phục
- Bản này dùng namespace localStorage `hant-preview-...` (được giữ nguyên khi chuyển nhánh preview sang `main`), độc lập với dữ liệu của HANT MVP cũ.
- **Dữ liệu HANT MVP cũ không tự chuyển sang cấu trúc mới**. Trước khi dùng với số liệu thật, hãy xuất bản sao lưu của ứng dụng cũ và kiểm tra kế hoạch chuyển đổi dữ liệu. Không nhập trực tiếp JSON cũ vào bản mới khi chưa có bộ chuyển đổi.
- Các thiết lập Google Sheets của ứng dụng cũ không tự được chuyển sang phiên bản này.
- Tạo bản sao lưu GitHub trước khi thay thế: `backup/hant-before-mobile-ntu-20261112`.

## Trạng thái kiểm thử
- Đã kiểm tra cú pháp JavaScript của `index.html` và `Code.gs`.
- Đã so sánh các hàm tính toán và tạo patch với preview gốc; không thay đổi.
- Chưa kiểm thử trực tiếp trên điện thoại thật và chưa xác minh cấu hình GitHub Pages. Trước khi kết nối dữ liệu thật, nên thử nhập liệu và tải file JSON.

## Lưu ý GitHub Pages
Nếu GitHub Pages hiện đang trỏ nhánh `preview/gold-mobile-original-engine`, nhánh preview đã có cập nhật giao diện NTU. Muốn website dùng nhánh chính mới, vào Settings → Pages và chọn `main`, thư mục `/(root)`.

Nguồn tham chiếu: https://github.com/tohanh1/hanh-kpi
