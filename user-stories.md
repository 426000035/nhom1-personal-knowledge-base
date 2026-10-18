# Danh sách User Stories - Đồ án Thiết kế Web

## Dự án: Hệ thống Kho lưu trữ Tài liệu cá nhân (Personal Knowledge Base)

* **Công nghệ cốt lõi:** HTML5, CSS3, JavaScript thuần (Vanilla JS), Google Sheets API (Google Apps Script), LocalStorage / IndexedDB.
* **Mục tiêu:** Xây dựng ứng dụng quản lý tài liệu cá nhân chạy trên trình duyệt (Single Page Application experience), có luồng tài khoản demo qua Google Apps Script/Google Sheets, hỗ trợ các định dạng tệp được liệt kê trong tài liệu này, tìm kiếm và ghi chú nhanh. Đăng nhập demo không phân vùng hoặc bảo vệ dữ liệu nội dung lưu cục bộ.

## PHÂN HỆ 1: XÁC THỰC VÀ TÀI KHOẢN NGƯỜI DÙNG (AUTHENTICATION - GOOGLE SHEETS)

### User Story 1.1: Đăng ký tài khoản mới qua Google Sheets
* **Mô tả:** Là một người dùng mới, tôi muốn nhập thông tin đăng ký để tạo tài khoản cá nhân, và dữ liệu này sẽ được lưu trữ trực tiếp lên Google Sheets (Cloud Database) của hệ thống.
* **Tiêu chí chấp nhận:**
  * Hiển thị form đăng ký trực quan (Tên đăng nhập, Mật khẩu, Email, v.v.).
  * JavaScript kiểm tra tính hợp lệ sơ bộ của dữ liệu trước khi gửi.
  * Sử dụng phương thức `fetch()` gọi API từ Google Apps Script để đẩy dữ liệu tài khoản mới lên Google Sheets.
  * Hiển thị thông báo đăng ký thành công hoặc báo lỗi nếu tên đăng nhập đã tồn tại trên hệ thống đám mây.

### User Story 1.2: Đăng nhập hệ thống qua Google Sheets
* **Mô tả:** Là một người dùng, tôi muốn nhập thông tin tài khoản và mật khẩu để xác thực với cơ sở dữ liệu đặt tại Google Sheets.
* **Tiêu chí chấp nhận:**
  * Form đăng nhập gửi yêu cầu kiểm tra xác thực thông qua API Google Apps Script.
  * Hệ thống quét dữ liệu trên Google Sheets để đối chiếu thông tin tài khoản và mật khẩu.
  * Nếu chính xác, lưu phiên đăng nhập vào `localStorage` và chuyển hướng sang Trang chủ. Nếu sai, hiển thị cảnh báo lỗi rõ ràng.

### User Story 1.3: Khôi phục mật khẩu trực tuyến
* **Mô tả:** Là một người dùng lỡ quên mật khẩu, tôi muốn thực hiện quy trình khôi phục demo và cập nhật mật khẩu mới thông qua Google Apps Script/Google Sheets sau khi xác minh OTP giả lập.
* **Tiêu chí chấp nhận:**
  * Có liên kết *"Quên mật khẩu?"* tại màn hình Đăng nhập.
  * Gửi OTP giả lập, kiểm tra OTP trước khi cho phép nhập mật khẩu mới và yêu cầu Google Apps Script cập nhật mật khẩu.
  * Ghi rõ trong giao diện demo rằng OTP không xác minh danh tính an toàn.
  * Hiển thị kết quả thành công hoặc lỗi từ dịch vụ; không báo thành công nếu cập nhật thất bại.

### User Story 1.4: Điều hướng theo phiên đăng nhập (Auth Guard)
* **Mô tả:** Là hệ thống demo, tôi cần điều hướng dựa trên phiên đăng nhập để kiểm soát luồng giao diện; cơ chế này không phải kiểm soát truy cập an toàn.
* **Tiêu chí chấp nhận:**
  * Các màn hình nội bộ kiểm tra trạng thái phiên demo trong `localStorage`.
  * Nếu chưa đăng nhập, điều hướng người dùng về màn hình đăng nhập.
  * Không tuyên bố Auth Guard phía client bảo vệ dữ liệu khỏi người dùng khác có quyền truy cập cùng hồ sơ trình duyệt.

### User Story 1.5: Đăng xuất hệ thống
* **Mô tả:** Là người dùng demo, tôi muốn bấm nút đăng xuất để kết thúc phiên đăng nhập hiện tại.
* **Tiêu chí chấp nhận:** Xóa trạng thái phiên demo và đưa người dùng quay lại màn hình đăng nhập; không xóa dữ liệu nội dung cục bộ.

## PHÂN HỆ 2: TRANG CHỦ (DASHBOARD)

### User Story 2.1: Hiển thị tổng quan tài liệu nổi bật
* **Mô tả:** Là một người dùng, tôi muốn xem ngay các tài liệu được xem nhiều nhất hoặc mới được thêm vào tại trang chủ để tiếp cận nhanh chóng thông tin quan trọng.
* **Tiêu chí chấp nhận:**
  * Giao diện phân chia rõ nhóm "Tài liệu mới thêm" và "Tài liệu xem nhiều".
  * Hiển thị dạng thẻ (Card view) trực quan với thông tin cơ bản (tiêu đề, định dạng, tag, ngày thêm, số lượt xem).
  * Click vào thẻ sẽ chuyển hướng sang Trang Chi Tiết tài liệu tương ứng.

### User Story 2.2: Truy cập nhanh các chức năng chính
* **Mô tả:** Là một người dùng, tôi muốn truy cập nhanh các chức năng thường dùng từ trang chủ để tiết kiệm thời gian thao tác.
* **Tiêu chí chấp nhận:**
  * Hiển thị các lối truy cập đến Kho tài liệu, Thêm tài liệu, Tạo ghi chú và Tìm kiếm.
  * Khi chọn một chức năng, hệ thống điều hướng đến giao diện tương ứng.
  * Các lối truy cập được bố trí rõ ràng và phù hợp với kích thước màn hình.

### User Story 2.3: Xem thống kê tổng quan kho tài liệu
* **Mô tả:** Là một người dùng, tôi muốn xem thống kê tổng quan về kho cá nhân để biết tình trạng tài liệu hiện có.
* **Tiêu chí chấp nhận:**
  * Hiển thị số lượng tài liệu và số lượng ghi chú độc lập riêng biệt.
  * Có thể thống kê tài liệu theo loại nội dung như tệp và URL.
  * Số liệu được cập nhật khi dữ liệu thay đổi.
  * Tài liệu đã xóa không được tính vào tổng số tài liệu đang hoạt động.

## PHÂN HỆ 3: KHO TÀI LIỆU VÀ QUẢN LÝ NỘI DUNG

### User Story 3.1: Chuyển đổi giao diện hiển thị (Card / List View)
* **Mô tả:** Là một người dùng, tôi muốn chuyển đổi qua lại giữa dạng thẻ (Card view) và dạng danh sách (List view) để quan sát tài liệu theo sở thích cá nhân.
* **Tiêu chí chấp nhận:** Có nút chuyển đổi trực quan (toggle button), thay đổi cách bố trí hiển thị của danh sách tài liệu ngay lập tức thông qua CSS Grid/Flexbox và JavaScript.

### User Story 3.2: Gợi ý tìm kiếm thông minh bằng thẻ `<datalist>`
* **Mô tả:** Là một người dùng, tôi muốn sử dụng ô tìm kiếm tích hợp thẻ `<datalist>` để nhận các gợi ý từ khóa hoặc định dạng file khi đang gõ.
* **Tiêu chí chấp nhận:** Ô input tìm kiếm liên kết với `<datalist>` tự động hiển thị danh sách các từ khóa hoặc định dạng phù hợp dựa trên dữ liệu hiện có.

### User Story 3.3: Lọc tài liệu theo Từ khóa, Định dạng và Tag (Không load lại trang)
* **Mô tả:** Là một người dùng, tôi muốn lọc tài liệu theo từ khóa, định dạng file (`PDF`, `Video`, `Link`, v.v.) hoặc Tag (nhãn) một cách mượt mà mà không bị tải lại trang.
* **Tiêu chí chấp nhận:**
  * Khi tương tác với bộ lọc (gõ từ khóa, chọn định dạng, click chọn tag badge), JavaScript xử lý lọc mảng dữ liệu và render lại danh sách ngay lập tức (SPA behavior).
  * Hiển thị thông báo rỗng thân thiện nếu không tìm thấy kết quả khớp.

### User Story 3.4: Thêm tài liệu vào kho
* **Mô tả:** Là một người dùng, tôi muốn thêm nội dung mới vào kho để tập trung lưu trữ và quản lý tài liệu cá nhân.
* **Tiêu chí chấp nhận:**
  * Cho phép thêm tệp từ thiết bị, lưu đường dẫn URL hoặc tạo ghi chú độc lập.
  * Cho phép nhập các thông tin mô tả như tên, mô tả và tag khi phù hợp với loại nội dung.
  * Kiểm tra các trường bắt buộc và thông báo khi dữ liệu không hợp lệ.
  * Thông báo kết quả thêm tài liệu thành công hoặc thất bại.
  * Tài liệu mới được hiển thị trong kho sau khi lưu thành công.

### User Story 3.5: Chỉnh sửa thông tin tài liệu
* **Mô tả:** Là một người dùng, tôi muốn chỉnh sửa thông tin mô tả của tài liệu để duy trì kho dữ liệu chính xác và có tổ chức.
* **Tiêu chí chấp nhận:**
  * Cho phép sửa các trường thông tin được hỗ trợ như tên, mô tả, tag và thư mục.
  * Dữ liệu sau khi lưu được cập nhật tại các giao diện liên quan.
  * Không thay đổi nội dung tệp gốc nếu người dùng chỉ chỉnh sửa thông tin mô tả.
  * Hiển thị thông báo khi lưu thành công hoặc xảy ra lỗi.

### User Story 3.6: Xóa tài liệu khỏi kho
* **Mô tả:** Là một người dùng, tôi muốn xóa tài liệu không còn cần thiết để giữ kho lưu trữ gọn gàng.
* **Tiêu chí chấp nhận:**
  * Có thao tác xóa tài liệu từ danh sách hoặc trang chi tiết.
  * Hiển thị yêu cầu xác nhận trước khi xóa.
  * Sau khi xóa thành công, tài liệu không còn xuất hiện trong danh sách đang hoạt động hoặc kết quả tìm kiếm.
  * Nếu tài liệu đang mở, hệ thống điều hướng về giao diện phù hợp sau khi xóa.
  * Thông báo rõ ràng nếu thao tác thất bại.

### User Story 3.7: Lưu và quản lý đường dẫn URL
* **Mô tả:** Là một người dùng, tôi muốn lưu đường dẫn đến nguồn kiến thức trực tuyến để quản lý tài liệu tham khảo cùng với các tài liệu cá nhân.
* **Tiêu chí chấp nhận:**
  * Cho phép nhập URL và tên hiển thị cho liên kết.
  * Kiểm tra URL có định dạng hợp lệ trước khi lưu.
  * Cho phép bổ sung mô tả và tag.
  * Hiển thị liên kết trong kho tài liệu và trang chi tiết.
  * Cho phép mở liên kết trong trình duyệt.
  * Thông báo khi URL không hợp lệ hoặc dữ liệu không thể lưu.

### User Story 3.8: Quản lý tag
* **Mô tả:** Là một người dùng, tôi muốn tạo và quản lý các tag để phân loại và tìm kiếm tài liệu theo chủ đề.
* **Tiêu chí chấp nhận:**
  * Cho phép gắn một hoặc nhiều tag cho một tài liệu.
  * Cho phép tạo và lựa chọn tag khi thêm hoặc chỉnh sửa tài liệu.
  * Hiển thị các tag trên giao diện danh sách hoặc chi tiết phù hợp.
  * Cho phép lọc tài liệu theo tag.
  * Tránh tạo các tag trùng nhau do khác biệt chữ hoa, chữ thường hoặc khoảng trắng không cần thiết.
  * Khi chỉnh sửa hoặc xóa tag, hệ thống xử lý các tài liệu liên quan nhất quán.

### User Story 3.9: Quản lý thư mục
* **Mô tả:** Là một người dùng, tôi muốn tổ chức tài liệu theo thư mục để dễ quản lý các nhóm nội dung.
* **Tiêu chí chấp nhận:**
  * Cho phép tạo, đổi tên và xóa thư mục.
  * Cho phép đưa tài liệu vào thư mục và thay đổi vị trí thư mục của tài liệu.
  * Hiển thị danh sách tài liệu thuộc thư mục được chọn.
  * Chỉ cho phép xóa thư mục rỗng; nếu còn tài liệu hoặc thư mục con, hướng dẫn người dùng di chuyển chúng trước khi xóa.
  * Không được xóa tài liệu hoặc thư mục con một cách âm thầm khi xóa thư mục.

### User Story 3.10: Sắp xếp tài liệu
* **Mô tả:** Là một người dùng, tôi muốn sắp xếp tài liệu theo các tiêu chí khác nhau để nhanh chóng tìm thấy nội dung cần thiết.
* **Tiêu chí chấp nhận:**
  * Hỗ trợ sắp xếp theo tên tài liệu, ngày thêm và ngày cập nhật.
  * Cho phép chọn thứ tự tăng dần hoặc giảm dần khi phù hợp.
  * Kết quả sắp xếp được cập nhật mà không tải lại toàn bộ trang.
  * Sắp xếp có thể kết hợp với các điều kiện tìm kiếm và lọc đang áp dụng.

### User Story 3.11: Phân trang hoặc giới hạn số lượng mục hiển thị
* **Mô tả:** Là một người dùng, tôi muốn kiểm soát số lượng tài liệu xuất hiện trên mỗi trang để dễ quan sát kho khi có nhiều dữ liệu.
* **Tiêu chí chấp nhận:**
  * Hệ thống hỗ trợ các lựa chọn 10, 20, 50 hoặc tất cả mục.
  * Khi phân trang, cho phép chuyển giữa các trang.
  * Kết quả tìm kiếm và lọc vẫn chính xác khi chuyển trang.
  * Khi dữ liệu thay đổi, hệ thống điều chỉnh trang hiện tại nếu trang đó không còn hợp lệ.

## PHÂN HỆ 4: CHI TIẾT TÀI LIỆU VÀ GHI CHÚ

### User Story 4.1: Xem nội dung chi tiết tài liệu
* **Mô tả:** Là một người dùng, tôi muốn xem nội dung chi tiết và khung hiển thị tương ứng khi chọn một tài liệu cụ thể từ danh sách.
* **Tiêu chí chấp nhận:** Đọc tham số ID từ URL (sử dụng `URLSearchParams`), tìm kiếm đúng tài liệu trong kho lưu trữ để hiển thị thông tin tiêu đề, ngày tạo, danh sách tag và vùng hiển thị nội dung phù hợp.

### User Story 4.2: Ghi chú nhanh (Quick Note) trên tài liệu
* **Mô tả:** Là một người dùng, tôi muốn viết và lưu các ghi chú cá nhân ngay tại trang chi tiết để ghi nhớ các điểm quan trọng của tài liệu.
* **Tiêu chí chấp nhận:**
  * Có khung nhập liệu (`textarea`) để viết ghi chú.
  * Nút lưu kích hoạt JavaScript ghi lại thông tin vào bộ nhớ cục bộ (không bị mất khi tải lại trang).
  * Hiển thị danh sách các ghi chú đã lưu bên dưới, cho phép người dùng thao tác chỉnh sửa hoặc xóa nhanh.

### User Story 4.3: Tạo ghi chú độc lập
* **Mô tả:** Là một người dùng, tôi muốn tạo ghi chú độc lập để lưu ý tưởng, kiến thức hoặc nội dung cần ghi nhớ mà không cần đính kèm tệp.
* **Tiêu chí chấp nhận:**
  * Cho phép nhập tiêu đề và nội dung ghi chú.
  * Cho phép bổ sung mô tả hoặc tag nếu được hỗ trợ.
  * Có thể lưu, mở, chỉnh sửa và xóa ghi chú.
  * Ghi chú được hiển thị trong Kho cùng danh sách tài liệu nhưng vẫn là entity `Note` riêng, không chuyển thành `Document`.
  * Nội dung đã lưu vẫn còn sau khi tải lại trang.

### User Story 4.4: Quản lý ghi chú gắn với tài liệu
* **Mô tả:** Là một người dùng, tôi muốn ghi lại nhận xét hoặc thông tin quan trọng liên quan đến một tài liệu để hỗ trợ việc học tập và nghiên cứu.
* **Tiêu chí chấp nhận:**
  * Cho phép tạo nhiều ghi chú cho một tài liệu nếu chức năng được hỗ trợ.
  * Các ghi chú được hiển thị trong trang chi tiết của tài liệu tương ứng, có highlight.
  * Cho phép chỉnh sửa và xóa từng ghi chú.
  * Nội dung ghi chú không bị nhầm lẫn với nội dung gốc của tệp.
  * Ghi chú được liên kết đúng với tài liệu tương ứng.

### User Story 4.5: Đánh dấu tài liệu yêu thích
* **Mô tả:** Là một người dùng, tôi muốn đánh dấu tài liệu yêu thích để truy cập nhanh các nội dung quan trọng.
* **Tiêu chí chấp nhận:**
  * Có thao tác thêm hoặc bỏ đánh dấu yêu thích.
  * Trạng thái yêu thích được hiển thị rõ ràng.
  * Cho phép lọc hoặc truy cập danh sách tài liệu yêu thích.
  * Trạng thái được giữ nguyên sau khi tải lại trang.

### User Story 4.6: Theo dõi trạng thái đọc
* **Mô tả:** Là một người dùng, tôi muốn đánh dấu trạng thái đọc của tài liệu để theo dõi tiến độ học tập và nghiên cứu.
* **Tiêu chí chấp nhận:**
  * Hỗ trợ các trạng thái như Chưa đọc, Đang đọc và Đã đọc.
  * Cho phép cập nhật trạng thái từ danh sách hoặc trang chi tiết.
  * Hiển thị trạng thái hiện tại của tài liệu.
  * Cho phép lọc tài liệu theo trạng thái đọc.

## PHÂN HỆ 5: QUẢN LÝ VÀ HIỂN THỊ ĐA ĐỊNH DẠNG TÀI LIỆU (DOCUMENT FORMAT RENDERING)

### User Story 5.1: Xem và chỉnh sửa văn bản/ghi chú (`.txt`, `.md`)
* **Mô tả:** Là một người dùng, tôi muốn xem nội dung, chỉnh sửa trực tiếp và render định dạng Markdown (`.md`) hoặc văn bản thuần (`.txt`) ngay trên trang chi tiết.
* **Tiêu chí chấp nhận:** Sử dụng thư viện `marked.js` để render cú pháp Markdown thành HTML trực quan; hỗ trợ chuyển đổi qua lại giữa chế độ Đọc (Preview) và Chỉnh sửa (Edit).

### User Story 5.2: Xem ảnh và phóng lớn (`.jpg`, `.jpeg`, `.png`, `.webp`, `.svg`)
* **Mô tả:** Là một người dùng, tôi muốn xem trước các file hình ảnh hoặc giấy tờ tùy thân, hỗ trợ phóng lớn (Lightbox) để quan sát rõ chi tiết.
* **Tiêu chí chấp nhận:** Hiển thị thumbnail trực tiếp bằng thẻ `<img>`; khi click vào ảnh sẽ kích hoạt hiệu ứng Lightbox phóng to toàn màn hình hoặc lớp phủ tối màu.

### User Story 5.3: Đọc và phân trang tài liệu PDF (`.pdf`)
* **Mô tả:** Là một người dùng, tôi muốn xem trực tiếp nội dung các tài liệu scan hoặc hợp đồng dạng PDF ngay trên trình duyệt kèm tính năng chuyển trang.
* **Tiêu chí chấp nhận:** Sử dụng thư viện **PDF.js** để nhúng và hiển thị file PDF; cung cấp nút điều hướng *Trang trước*, *Trang sau* và hiển thị tổng số trang.

### User Story 5.4: Chuyển đổi và đọc trực tiếp file Word (`.docx`)
* **Mô tả:** Là một người dùng, tôi muốn hệ thống tự động đọc và chuyển đổi nội dung file Word (`.docx`) thành văn bản HTML để đọc trực tiếp trên web.
* **Tiêu chí chấp nhận:** Sử dụng thư viện **mammoth.js** ở phía client để đọc file `.docx` và render cấu trúc văn bản ra giao diện HTML mượt mà.

### User Story 5.5: Hiển thị bảng tính Excel dưới dạng bảng biểu (`.xlsx`, `.xls`, `.csv`)
* **Mô tả:** Là một người dùng, tôi muốn xem trước dữ liệu từ các file bảng tính dưới dạng bảng biểu (`<table>`) gọn gàng và trực quan.
* **Tiêu chí chấp nhận:** Sử dụng thư viện **SheetJS (xlsx)** để phân tích dữ liệu file và tự động chuyển đổi thành các thẻ `<table>`, `<tr>`, `<td>` của HTML.

### User Story 5.6: Đọc sách điện tử với tính năng lật trang (`.epub`)
* **Mô tả:** Là một người dùng, tôi muốn đọc sách điện tử (`.epub`) trực tiếp trên hệ thống, có hỗ trợ lật trang và tùy chỉnh giao diện đọc sách.
* **Tiêu chí chấp nhận:** Sử dụng thư viện **epub.js** để render nội dung sách điện tử; cung cấp bảng điều khiển lật qua lại giữa các chương/trang sách.

### User Story 5.7: Phát và điều khiển trực tiếp file Media Video (`.mp4`, `.webm`)
* **Mô tả:** Là một người dùng, tôi muốn phát trực tiếp các video hướng dẫn hoặc bài giảng ngay trên hệ thống với đầy đủ tính năng điều khiển.
* **Tiêu chí chấp nhận:** Sử dụng thẻ `<video>` chuẩn của HTML5 kèm đầy đủ thanh điều khiển (Play/Pause, Seekbar, Volume, Fullscreen).

## PHÂN HỆ 6: QUẢN LÝ TỆP TẢI LÊN

### User Story 6.1: Tải tệp từ thiết bị vào kho
* **Mô tả:** Là một người dùng, tôi muốn chọn tệp từ thiết bị để lưu trữ và quản lý trong kho tài liệu cá nhân.
* **Tiêu chí chấp nhận:**
  * Cho phép chọn tệp từ thiết bị thông qua giao diện tải tệp.
  * Hiển thị tên và thông tin cơ bản của tệp trước khi lưu.
  * Chỉ chấp nhận các phần mở rộng được liệt kê trong `data-contract.md` và kiểm tra giới hạn dung lượng theo hợp đồng dữ liệu.
  * Thông báo khi tệp không được hỗ trợ hoặc vượt quá giới hạn.
  * Chỉ thông báo thành công khi dữ liệu đã được lưu thành công.
  * Xử lý trường hợp người dùng hủy thao tác hoặc trình duyệt không đủ dung lượng lưu trữ.

### User Story 6.2: Cập nhật tệp tài liệu
* **Mô tả:** Là một người dùng, tôi muốn thay thế tệp đã lưu bằng phiên bản mới khi cần cập nhật nội dung.
* **Tiêu chí chấp nhận:**
  * Cho phép chọn tệp mới để thay thế tệp hiện tại.
  * Hiển thị thông tin tệp mới trước khi xác nhận.
  * Yêu cầu xác nhận trước khi thay thế dữ liệu hiện tại.
  * Nếu thay thế thất bại, dữ liệu cũ không bị mất ngoài ý muốn.

### User Story 6.3: Xử lý tệp không thể xem trước
* **Mô tả:** Là một người dùng, tôi muốn nhận thông báo rõ ràng khi một tệp không thể hiển thị trực tiếp để biết cách tiếp tục sử dụng tệp đó.
* **Tiêu chí chấp nhận:**
  * Hiển thị thông tin về loại tệp và tình trạng hỗ trợ.
  * Nếu phù hợp, cung cấp thao tác tải tệp về thiết bị.
  * Không làm hỏng dữ liệu gốc chỉ vì quá trình xem trước thất bại.
  * Thông báo lỗi dễ hiểu, không chỉ hiển thị thông báo lỗi kỹ thuật.

## PHÂN HỆ 7: CÁ NHÂN HÓA GIAO DIỆN

### User Story 7.1: Tùy chỉnh giao diện sáng và tối
* **Mô tả:** Là một người dùng, tôi muốn chuyển đổi giao diện sáng hoặc tối để phù hợp với điều kiện sử dụng.
* **Tiêu chí chấp nhận:**
  * Có điều khiển chuyển đổi giữa các giao diện được hỗ trợ.
  * Các thành phần chính của giao diện cập nhật nhất quán.
  * Lựa chọn được giữ nguyên khi người dùng quay lại ứng dụng.

### User Story 7.2: Ghi nhớ tùy chọn hiển thị
* **Mô tả:** Là một người dùng, tôi muốn hệ thống ghi nhớ các tùy chọn hiển thị để không phải thiết lập lại mỗi lần sử dụng.
* **Tiêu chí chấp nhận:**
  * Có thể ghi nhớ các tùy chọn được ứng dụng hỗ trợ, chẳng hạn Card/List hoặc số mục hiển thị.
  * Khi mở lại ứng dụng, các tùy chọn được khôi phục phù hợp.
  * Nếu dữ liệu tùy chọn không hợp lệ, ứng dụng sử dụng giá trị mặc định và vẫn hoạt động bình thường.

## PHÂN HỆ 8: AN TOÀN DỮ LIỆU VÀ XỬ LÝ LỖI

### User Story 8.1: Xác nhận thao tác có nguy cơ mất dữ liệu
* **Mô tả:** Là một người dùng, tôi muốn được cảnh báo trước những thao tác có thể làm mất dữ liệu để tránh xóa hoặc ghi đè ngoài ý muốn.
* **Tiêu chí chấp nhận:**
  * Hiển thị xác nhận trước các thao tác xóa hoặc thay thế dữ liệu quan trọng.
  * Nêu rõ đối tượng sẽ bị ảnh hưởng.
  * Chỉ thực hiện thao tác sau khi người dùng xác nhận.
  * Nếu người dùng hủy, dữ liệu hiện tại được giữ nguyên.

### User Story 8.2: Thông báo lỗi lưu dữ liệu
* **Mô tả:** Là một người dùng, tôi muốn được thông báo khi hệ thống không thể lưu dữ liệu để biết thao tác đã hoàn thành hay chưa.
* **Tiêu chí chấp nhận:**
  * Hiển thị trạng thái thành công hoặc thất bại sau thao tác lưu.
  * Không thông báo thành công khi dữ liệu chưa được lưu.
  * Giữ lại nội dung người dùng đang nhập khi có thể nếu thao tác lưu thất bại.
  * Cung cấp hướng dẫn phù hợp để người dùng thử lại hoặc xử lý lỗi.

### User Story 8.3: Xử lý dữ liệu trống và dữ liệu không hợp lệ
* **Mô tả:** Là một người dùng, tôi muốn ứng dụng xử lý dữ liệu trống hoặc không hợp lệ một cách rõ ràng để tránh lỗi trong quá trình sử dụng.
* **Tiêu chí chấp nhận:**
  * Hiển thị trạng thái phù hợp khi kho chưa có tài liệu.
  * Hiển thị thông báo khi tìm kiếm không có kết quả.
  * Kiểm tra dữ liệu bắt buộc trước khi lưu.
  * Không để dữ liệu không hợp lệ làm gián đoạn các chức năng khác.

### User Story 8.4: Làm rõ giới hạn dữ liệu giữa các tài khoản
* **Mô tả:** Là người dùng demo, tôi muốn được thông báo rõ giới hạn của dữ liệu cục bộ để không nhầm đăng nhập với cơ chế bảo vệ hoặc phân tách dữ liệu theo tài khoản.
* **Tiêu chí chấp nhận:**
  * Giao diện/tài liệu demo nói rõ nội dung trong IndexedDB được dùng chung trong cùng hồ sơ trình duyệt.
  * Đăng xuất không xóa nội dung cục bộ và cũng không làm nội dung đó trở nên riêng tư với tài khoản khác trên cùng hồ sơ trình duyệt.
  * Không tuyên bố rằng đăng nhập demo cung cấp kiểm soát truy cập hoặc cách ly dữ liệu.

## PHÂN HỆ 9: TRÍ TUỆ NHÂN TẠO VÀ TRỰC QUAN HÓA TRI THỨC (SECOND BRAIN)

### User Story 9.1: Tự động tóm tắt tài liệu bằng AI (AI Document Summary)
* **Mô tả:** Là một người dùng, tôi muốn hệ thống tự động trích xuất và tóm tắt ngắn gọn nội dung cốt lõi của tài liệu (PDF, văn bản, bài viết) bằng AI để tiết kiệm thời gian đọc hiểu.
* **Tiêu chí chấp nhận:**
  * Có nút/tính năng *"Tóm tắt bằng AI"* tại trang chi tiết tài liệu.
  * Hệ thống xử lý nội dung văn bản và hiển thị khung kết quả tóm tắt (bao gồm: Ý chính, Các từ khóa quan trọng, và Bullet points tổng hợp).
  * Cho phép người dùng lưu lại bản tóm tắt này như một ghi chú nhanh liên kết trực tiếp với tài liệu.
  * Gửi yêu cầu đến API AI thật thông qua lớp trung gian phía máy chủ; không gọi nhà cung cấp bằng khóa bí mật từ trình duyệt.
  * Hiển thị trạng thái đang xử lý và lỗi rõ ràng nếu dịch vụ không khả dụng hoặc phản hồi không hợp lệ.

### User Story 9.2: Gợi ý và liên kết ý tưởng chéo (Smart Note Linking)
* **Mô tả:** Là một người dùng, tôi muốn liên kết các ghi chú hoặc tài liệu có chung chủ đề lại với nhau để tạo thành mạng lưới tri thức liên kết (Backlinks / Connected Notes).
* **Tiêu chí chấp nhận:**
  * Khi viết ghi chú hoặc xem chi tiết, cho phép người dùng gõ cú pháp liên kết nhanh (ví dụ: gõ `[[Tên tài liệu/Ghi chú khác]]`) để tạo cầu nối tri thức giữa các mục.
  * Hiển thị danh sách các "Tài liệu liên quan" hoặc "Backlinks" ở lề trang chi tiết để dễ dàng tra cứu chéo.

### User Story 9.3: Trực quan hóa sơ đồ liên kết tri thức (Knowledge Graph / Mindmap View)
* **Mô tả:** Là một người dùng, tôi muốn quan sát toàn bộ kho tài liệu, tag và ghi chú dưới dạng một sơ đồ mạng lưới nút giao (Graph view) để thấy được bức tranh tổng quan về các mối quan hệ giữa các chủ đề kiến thức.
* **Tiêu chí chấp nhận:**
  * Cung cấp một trang/tab riêng biệt hiển thị **Sơ đồ liên kết (Knowledge Graph)** bằng thư viện `vis-network` theo quyết định kiến trúc.
  * Mỗi tài liệu, tag hoặc ghi chú xuất hiện như một "nút" (node), các mối liên hệ (tag chung, liên kết backlink) xuất hiện như các "đường nối" (edge).
  * Cho phép người dùng tương tác với sơ đồ: Phóng to/thu nhỏ, kéo thả các nút, và click vào một nút bất kỳ để mở nhanh tài liệu tương ứng.