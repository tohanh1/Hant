# HANT — KPI Workspace

Workspace KPI độc lập, thiết kế theo concept **Midnight Ledger**: xanh than, xanh mint và điểm nhấn lime. Responsive cho desktop và mobile.

## Chạy thử
Mở `index.html` bằng trình duyệt. Có thể bật GitHub Pages từ Settings → Pages → Deploy from branch → main → /(root).

## Tính năng MVP
- Dashboard KPI tổng hợp COF, NON, POS quy đổi, NTU và tiến độ mục tiêu.
- Quản lý khoản thu theo loại thu và hệ số POS.
- Quản lý hồ sơ NTU, trạng thái mindue và tiền thu.
- Ước tính bonus, trách nhiệm NTU và thu nhập sau thuế theo bảng hệ số tham chiếu.
- Cấu hình target, kỳ KPI, khoản cố định, người phụ thuộc và bảo hiểm.
- Lưu dữ liệu trên trình duyệt, undo/redo, xuất/nhập JSON.

## Giới hạn hiện tại
- Đây là bản MVP độc lập; chưa kết nối Google Sheets và chưa đồng bộ đa thiết bị.
- Dữ liệu lưu trong localStorage của trình duyệt. Nên xuất bản sao lưu định kỳ.
- Các bảng tính KPI/thuế là logic tham chiếu từ dự án trước, cần đối chiếu chính sách nội bộ trước khi dùng để chốt thu nhập.
- Chưa có kiểm thử thực tế trên nhiều thiết bị/trình duyệt.
