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


## Tự động xếp khoản thu trên MIX 1 NEW (hàng 8–60)

Đã bổ sung xử lý nhập/sửa từ Sheet và HANT Web App. Thu kỳ được dồn từ hàng 8 xuống; Thanh lý, Thu quá hạn, Ngoại lệ được xếp từ hàng 60 lên theo thứ tự nhóm. **Tính năng trong Google Sheet chỉ hoạt động sau khi cập nhật và triển khai lại dự án Apps Script cùng trigger được cấp quyền**; cập nhật GitHub hoặc Pages một mình không đủ.

Hướng dẫn bật, sao lưu, thử nghiệm và khôi phục: [HUONG-DAN-SAP-XEP.md](./HUONG-DAN-SAP-XEP.md).


## Nâng cấp tháng mới, định dạng NTU và Thu 1.0

- **Bắt đầu tháng mới:** cần đồng bộ Google Sheets. Trước khi Reset, ứng dụng xuất bản sao JSON và Apps Script tạo tab sao lưu ẩn `BACKUP MIX yyyyMMdd-HHmmss`. Chỉ báo thành công khi API xác nhận Reset.
- **Thu tiền A8:E60:** giữ tất cả tên ở A, đưa B về `Thu kỳ`, xóa C:D, cột E phục hồi công thức POS.
- **NTU G:Q:** xóa **giá trị** trong G:N và Q, giữ mọi công thức, bao gồm O:P, J và Q nếu có. Không đổi cấu trúc bảng.
- **Targets:** xóa Target COF, Target NON, Target NTU và NTU CIC OK; giữ các thiết lập khác.
- **Thu 1.0:** hệ số POS COF = 1,0 và NON = 1,0. Sheet `HANH 2026 / MIX 1 NEW` đã được cập nhật danh sách kiểu thu và bảng hệ số; không tác động dữ liệu hồ sơ.
- **Cột P:** chỉ làm nổi bật ô trạng thái bằng xanh lá/xanh dương/cam/xám. C:D không còn bị phủ bởi quy tắc tô xanh theo hàng của A8:E60.
- **An toàn đồng bộ:** mỗi lần Reset tăng mã phiên kỳ; ứng dụng khác phải tải lại dữ liệu kỳ mới trước khi ghi. Phiên bản ứng dụng và Apps Script **phải cập nhật cùng nhau**.

### Kích hoạt phiên bản mới

**GitHub Pages chỉ cập nhật giao diện PWA, không cập nhật Apps Script Google Sheets.** Cập nhật `Code.gs` trong dự án Apps Script đang kết nối với `HANH 2026`, giữ nguyên token bí mật đang dùng. Sau đó, trong Apps Script chọn **Triển khai → Quản lý hoạt động triển khai → Chỉnh sửa → Phiên bản mới → Triển khai**. Kiểm tra URL đồng bộ và thực hiện thử Reset trên một **bản sao** của Sheet trước khi dùng trên dữ liệu thật.

**Chú ý:** `Code.gs` trên GitHub chứa token mẫu, không tự bảo mật hay vận hành được nếu chưa cấu hình Apps Script. Không đưa token thật vào repo công khai. Nếu Apps Script chưa cập nhật, nút Reset sẽ từ chối nhận thành công và không tự xóa dữ liệu cục bộ.

Bản sao lưu mã trước thay đổi: `backup/hant-before-month-reset-20261121`.
