# Tự xếp khoản thu MIX 1 NEW — hàng 8–60

Áp dụng cho **HANT Pro** và tab **MIX 1 NEW** trong Google Sheet. Tính năng nằm trong `Code.gs` và `index.html` của bản phát hành mới.

## Quy tắc
- **Thu kỳ:** từ hàng 8 đi xuống.
- **Thanh lý** (B3–B12, Thanh lý COF): từ hàng 60 đi lên.
- **Thu quá hạn:** nằm ngay phía trên nhóm Thanh lý.
- **Ngoại lệ:** nằm phía trên nhóm Thu quá hạn.
- Hàng trống để ở giữa nếu còn chỗ.
- Không dịch chuyển hoặc sắp xếp hàng 61 trở đi, phần NTU và chỉ tiêu ở các cột G trở đi.

## Tính an toàn
- Cột A:D: chỉ di chuyển **giá trị**, không dịch chuyển định dạng hay xác thực dữ liệu; không thực hiện nếu có công thức A:D hoặc ghi chú trong A:E.
- Cột E: công thức R1C1 giữ theo **hàng đích**; trường hợp Ngoại lệ hoặc khoản chỉ tính POS có E giá trị nhập tay sẽ đi cùng hồ sơ; vị trí E trở về loại thường được khôi phục công thức.
- Bảo toàn những ô **loại thu mặc định** ở các dòng trống (ví dụ Thu kỳ hoặc Thanh lý B3), không coi đó là khoản thu.
- Nếu tiêu đề không nằm tại hàng 7 và phần khách hàng không kết thúc ở hàng 60, dừng xử lý để bảo vệ dữ liệu.
- Gắn ID kỹ thuật ổn định theo mỗi khoản thu, không ghi ID vào vùng ô của Sheet. Khi đổi hàng, HANT đồng bộ theo ID thay vì chỉ theo số hàng.
- Có phương án hoàn tác bằng dữ liệu lưu trong bộ nhớ nếu lỗi trong lúc sắp xếp. Vẫn cần **tạo bản sao lưu Google Sheet trước khi bật**.
- HANT từ chối gửi các thao tác sửa/xóa theo số hàng cũ nếu chưa xác định ID tương ứng.

## Cách kích hoạt trên Google Sheets thật
1. Mở Google Sheet **HANH 2026**, chọn **Tệp → Tạo bản sao** để có bản dự phòng (quan trọng).
2. Mở tab **MIX 1 NEW → Tiện ích mở rộng → Apps Script**.
3. Cập nhật toàn bộ mã trong `Code.gs` từ repository HANT Pro. **Giữ lại đúng token đồng bộ bí mật** và thiết lập `CFG.SHEET: 'MIX 1 NEW'` từ phiên bản Apps Script đang chạy, không sử dụng token ví dụ trong GitHub.
4. Lưu dự án, mở danh sách hàm và chọn `installMixAutoSortTrigger`, nhấn **Run/Chạy**. Chấp thuận quyền theo hướng dẫn Google. Hàm này tạo một trigger sắp xếp chỉ một lần. Việc cài trigger cần thực hiện trên project Apps Script đang gắn với đúng Google Sheet.
5. Trở lại Google Sheets, tải lại trang. Menu **HANH KPI** sẽ có **Sắp xếp thu tiền ngay** để sắp lại những hồ sơ cũ trong hàng 8–60. Sau khi đã sao lưu, chạy lệnh này một lần và kiểm tra kết quả.
6. Để bản web HANT Pro sử dụng API mới, vào **Apps Script → Triển khai → Quản lý hoạt động triển khai → Chỉnh sửa**, chọn **Phiên bản mới**, rồi triển khai. Nếu URL Apps Script giữ nguyên, HANT vẫn kết nối như cũ.
7. Tải lại HANT bằng tab mới để nhận `index.html` mới. Thử một khoản thu kỳ và một khoản thanh lý nhỏ hoặc dữ liệu thử trên bản sao Sheet trước khi đưa vào sử dụng.

**Lưu ý:** Chỉ cập nhật GitHub hoặc GitHub Pages **không** tự cập nhật phiên bản `Code.gs` đã triển khai trong Apps Script. Cần các bước trên để Google Sheet và HANT tự sắp xếp thực sự.

## Nếu có lỗi
- Nếu ứng dụng báo hồ sơ trùng/đã đổi vị trí hoặc lỗi đồng bộ, **không tiếp tục nhập khoản thu mới** cho đến khi đối chiếu dữ liệu.
- Tải JSON dự phòng HANT, kiểm tra bản sao Sheet, đừng sử dụng thao tác xóa nhanh để xử lý lỗi.
- Có thể tắt trigger `handleMixPaymentEdit` tại **Apps Script → Triggers**, dùng nhánh sao lưu trên GitHub để quay lại code cũ.
- Khi hoàn tác Apps Script, cũng cần xuất bản lại deployment mới sau khi phục hồi source.

## Kiểm thử đã thực hiện
- Đối chiếu **bản sao dữ liệu đọc** của `HANH 2026 / MIX 1 NEW / A8:E60`: **25** khoản thu có dữ liệu, tổng COF+NON **61.760.000 đồng** trước và sau mô phỏng.
- Bản mô phỏng đưa 22 Thu kỳ lên hàng 8–29, Ngoại lệ hàng 58, Thanh lý hàng 59–60.
- 52 ô chứa công thức E vẫn giữ 52 công thức; 1 ô E nhập tay giữ giá trị.
- Đã kiểm tra trường hợp trang tính không đúng phạm vi, có công thức không được di chuyển, và đồng bộ theo ID khi vị trí hồ sơ đổi.
- **Chưa thực hiện sắp xếp hoặc cài trigger trên Google Sheet thật**; không có dữ liệu công việc nào bị di chuyển trong quá trình xây dựng mã.
