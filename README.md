# HANT – Preview: Vàng Champagne + nghiệp vụ HANH KPI gốc

**Bản xem trước nằm trong nhánh** `preview/gold-mobile-original-engine`, chưa thay đổi `main`.

## Khác biệt so với HANT hiện tại
- Dùng lại mã nguồn nghiệp vụ gốc `hanh-kpi/main/index.html` thay vì tính lại bằng mô hình HANT MVP.
- Trang Thu tiền hiển thị mỗi khoản thành một dòng tóm tắt trên điện thoại; chạm để mở chi tiết và chỉnh sửa.
- Phối màu vàng champagne, trắng ngà; hỗ trợ dark mode.
- Target NTU (`tNTU`), NTU CIC OK (`ntuOK`) và hồ sơ đạt mindue (`okN`) được giữ tách biệt.
- Không còn đổi trạng thái "đang đồng bộ" khi đồng bộ nền thành công.

## Tệp đi kèm
- `index.html`: giao diện preview với engine gốc, chưa thay đổi công thức.
- `Code.gs`: Apps Script gốc để đối chiếu và triển khai độc lập khi cần, **không tự kết nối Sheet**.
- `sw.js`: cache tài nguyên tĩnh, bỏ qua URL có query string.
- `manifest.webmanifest`: khai báo ứng dụng xem trước.

## Giới hạn và an toàn
- LocalStorage được tách bằng tiền tố `hant-preview-` để tránh ghi đè dữ liệu HANT MVP.
- Mặc định chưa có kết nối Google Sheets. Nếu người dùng tự nhập cấu hình đồng bộ vào preview, dữ liệu có thể được ghi lên Sheet thật.
- Chưa có kiểm thử bằng trình duyệt iPhone, Google Sheets thật hay quy trình đồng bộ nhiều thiết bị.
- GitHub Pages chưa được xác minh đã bật; nhánh preview **không tự động tạo URL website**.
- Chỉ merge sau khi hoàn tất thử nghiệm.

## Mã tham chiếu
Nguồn logic: https://github.com/tohanh1/hanh-kpi/blob/main/index.html
