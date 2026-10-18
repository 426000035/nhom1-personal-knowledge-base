# Project Skills

## 1. Mục đích và thứ tự ưu tiên

Tài liệu này hướng dẫn AI thực hiện các quy trình phát triển, kiểm thử và tích hợp cho Personal Knowledge Base. Đây là quy trình làm việc, không thay thế đặc tả tính năng hoặc hợp đồng dữ liệu.

Trước khi thực hiện một yêu cầu, tham khảo:

- `AGENTS.md` trong thư mục `.ai/` để biết quy tắc làm việc chung.
- `../architecture.md` để biết màn hình, luồng chức năng và các quyết định kỹ thuật đã chốt.
- `../data-contract.md` để biết cấu trúc dữ liệu, quan hệ, lưu trữ và quy tắc nghiệp vụ.
- `../user-stories.md` để biết yêu cầu và tiêu chí chấp nhận của tính năng.

Nếu các tài liệu mâu thuẫn hoặc yêu cầu mới làm thay đổi phạm vi đã chốt, hãy nêu rõ mâu thuẫn và báo người dùng trước khi thay đổi hợp đồng, tài liệu hoặc hành vi hiện có. Không tự mở rộng phạm vi.

## 2. Skill: Thực hiện một tính năng

### Mục tiêu
Hoàn thành tính năng được yêu cầu mà không làm hỏng chức năng hiện có.

### Quy trình

1. Xác định yêu cầu, người dùng mục tiêu và tiêu chí chấp nhận.
2. Xác định màn hình, mô-đun, dịch vụ và dữ liệu liên quan.
3. Đọc các phần phù hợp trong `architecture.md` và `data-contract.md`.
4. Kiểm tra cấu trúc mã hiện có và tìm dịch vụ hoặc thành phần có thể tái sử dụng.
5. Xác định các tệp cần thay đổi trước khi chỉnh sửa.
6. Triển khai theo cấu trúc HTML, CSS và JavaScript hiện có; không thêm framework hoặc bước build nếu chưa được phê duyệt.
7. Kiểm tra đầu vào và xử lý rõ trạng thái đang tải, thành công, rỗng và lỗi.
8. Cập nhật tài liệu liên quan nếu thay đổi luồng chức năng hoặc hợp đồng dữ liệu.
9. Chạy kiểm thử nhỏ nhất phù hợp và kiểm tra hồi quy các luồng bị ảnh hưởng.

### Tiêu chí hoàn thành

- Tính năng đáp ứng yêu cầu và tiêu chí chấp nhận.
- Dữ liệu tuân theo `data-contract.md`.
- Không tạo dịch vụ hoặc logic trùng lặp khi đã có giải pháp dùng chung.
- Lỗi được thông báo rõ ràng; không giả lập thành công khi thao tác thất bại.
- Các luồng liên quan tiếp tục hoạt động.

## 3. Skill: Thay đổi dữ liệu IndexedDB

### Mục tiêu
Duy trì dữ liệu ứng dụng nhất quán và có thể đọc lại sau khi tải lại trang.

### Quy trình

1. Xác định entity, quan hệ và thao tác CRUD bị ảnh hưởng.
2. Đối chiếu cấu trúc và quy tắc với `data-contract.md`.
3. Kiểm tra các mô-đun đang đọc hoặc ghi dữ liệu đó.
4. Dùng dịch vụ dữ liệu hiện có; không để từng màn hình tự tạo cơ chế lưu trữ riêng.
5. Thực hiện các cập nhật liên quan theo cách giữ tính nhất quán của dữ liệu.
6. Nếu cần đổi schema hoặc chuyển đổi dữ liệu cũ, xác định kế hoạch tương thích trước khi triển khai.
7. Xử lý rõ IndexedDB không khả dụng, đầy dung lượng, giao dịch lỗi hoặc bản ghi không tồn tại.
8. Kiểm tra tạo, đọc, cập nhật, xóa, tải lại trang và các tham chiếu liên quan.

### Quy tắc

- Dùng IndexedDB cho dữ liệu nội dung và tệp tải lên theo hợp đồng dữ liệu.
- Không lưu nội dung tệp lớn trong localStorage.
- Giữ localStorage cho phiên đăng nhập và các tùy chọn nhỏ theo kiến trúc đã chốt.
- Không xóa dữ liệu người dùng để xử lý lỗi mặc định.
- Khi xóa hoặc sửa entity, xử lý các liên kết, ghi chú, highlight và trạng thái liên quan theo `data-contract.md`.
- Chỉ báo lưu thành công sau khi giao dịch lưu hoàn tất.

## 4. Skill: Tích hợp API AI

### Mục tiêu
Kết nối tính năng tóm tắt và gợi ý tri thức với API AI thật một cách an toàn, có thể xử lý lỗi.

### Quy trình

1. Xác định tác vụ AI cụ thể: tóm tắt tài liệu hay đề xuất liên kết tri thức.
2. Chỉ gửi dữ liệu tối thiểu cần thiết cho tác vụ đó.
3. Gửi yêu cầu qua lớp trung gian phía máy chủ đã được kiến trúc quy định.
4. Không gọi API AI có khóa bí mật trực tiếp từ JavaScript phía trình duyệt.
5. Kiểm tra dữ liệu phản hồi trước khi hiển thị hoặc lưu.
6. Hiển thị trạng thái đang xử lý và lỗi dễ hiểu; cho phép người dùng thử lại khi phù hợp.
7. Chỉ lưu bản tóm tắt thành ghi chú khi người dùng yêu cầu và thao tác lưu thành công.
8. Kiểm thử phản hồi hợp lệ, phản hồi rỗng/sai định dạng, lỗi mạng và lỗi từ nhà cung cấp.

### Quy tắc

- AI tóm tắt và AI gợi ý Knowledge Graph là các chức năng gọi API thật theo kiến trúc hiện tại.
- Không trình bày nội dung AI như dữ kiện đã xác minh.
- Gợi ý AI không phải quan hệ chính thức trong Knowledge Graph cho đến khi người dùng chấp nhận.
- Không dùng kết quả AI để tự ý tạo, sửa hoặc xóa dữ liệu.
- Không ghi khóa API, token hoặc thông tin nhạy cảm vào mã nguồn, log phía trình duyệt hay tài liệu.

## 5. Skill: Xây dựng và cập nhật Knowledge Graph

### Mục tiêu
Hiển thị quan hệ tri thức rõ ràng, phân biệt quan hệ đã xác nhận với gợi ý AI.

### Quy trình

1. Đọc entity và quan hệ được định nghĩa trong `data-contract.md`.
2. Lấy dữ liệu đồ thị qua dịch vụ dùng chung; không tạo bản sao dữ liệu nội dung trong mô-đun graph.
3. Dựng các node từ tài liệu, ghi chú và tag; dựng các cạnh từ quan hệ đã có và đã xác nhận.
4. Hiển thị gợi ý AI tách biệt với cạnh chính thức.
5. Cho phép người dùng chấp nhận hoặc từ chối từng gợi ý.
6. Chỉ tạo quan hệ chính thức sau khi người dùng chấp nhận và lưu thành công.
7. Dùng vis-network theo quyết định trong `architecture.md`; không thêm bước build hoặc framework.
8. Hỗ trợ phóng to/thu nhỏ, kéo thả, lọc và mở entity khi chọn node.
9. Kiểm tra entity không tồn tại, node trùng, quan hệ tự tham chiếu, gợi ý bị từ chối và lỗi lưu.

### Quy tắc

- Tag và ghi chú liên kết với tài liệu có thể được suy ra từ quan hệ dữ liệu hiện có; tránh tạo liên kết trùng lặp.
- Không tự động xác nhận gợi ý AI.
- Khi xóa entity, loại bỏ hoặc xử lý các liên kết và gợi ý tham chiếu đến entity đó theo hợp đồng dữ liệu.
- Cung cấp trạng thái rỗng và thông báo lỗi nếu không thể dựng đồ thị.

## 6. Skill: Kiểm thử và gỡ lỗi

### Mục tiêu
Xác minh hành vi mong đợi, lỗi biên và tính toàn vẹn dữ liệu trước khi hoàn tất.

### Quy trình

1. Ghi lại hành vi mong đợi và cách tái hiện.
2. Kiểm tra luồng thành công chính.
3. Kiểm tra dữ liệu trống, đầu vào sai và tham chiếu không tồn tại.
4. Kiểm tra lỗi lưu trữ, lỗi mạng hoặc lỗi API liên quan.
5. Kiểm tra dữ liệu vẫn đọc được sau khi tải lại trang.
6. Kiểm tra thao tác xóa, khôi phục hoặc thay thế có xác nhận khi cần.
7. Kiểm tra các màn hình và mô-đun phụ thuộc để tìm hồi quy.
8. Báo cáo rõ kiểm thử đã chạy, kết quả và giới hạn còn lại.

### Trường hợp cần kiểm tra khi liên quan

- Phân trang: 10, 20, 50 và tất cả; giá trị mặc định là 10.
- Dashboard: danh sách tài liệu mới thêm và vừa mới xem.
- Ghi chú: nhiều ghi chú cùng liên kết với một tài liệu.
- Khôi phục mật khẩu: luồng OTP giả lập, OTP sai và cập nhật mật khẩu thất bại.
- AI: loading, kết quả hợp lệ, lỗi API và lỗi lưu ghi chú.
- Knowledge Graph: liên kết đã xác nhận và gợi ý đang chờ/từ chối.
- Tệp: định dạng không hỗ trợ, vượt giới hạn hoặc IndexedDB hết dung lượng.

## 7. Skill: Tích hợp mô-đun

### Mục tiêu
Kết nối tính năng mới với điều hướng, dịch vụ và giao diện hiện có mà không phá vỡ hành vi khác.

### Quy trình

1. Kiểm tra cấu trúc ứng dụng và điểm vào điều hướng hiện tại.
2. Tìm thành phần, CSS, dịch vụ và tiện ích dùng chung.
3. Đối chiếu dữ liệu với `data-contract.md`.
4. Giữ rõ ranh giới giữa giao diện, nghiệp vụ và lưu trữ.
5. Tránh CSS toàn cục hoặc biến toàn cục nếu không theo mẫu hiện có.
6. Kiểm tra liên kết điều hướng, trạng thái tải, lỗi và dữ liệu rỗng.
7. Chạy kiểm thử mô-đun và hồi quy các mô-đun liên quan.

### Tiêu chí hoàn thành

- Người dùng truy cập được chức năng qua điều hướng phù hợp.
- Dữ liệu được chia sẻ nhất quán qua dịch vụ hiện có.
- Không có logic lưu trữ hoặc xử lý nghiệp vụ bị nhân đôi.
- Không làm hỏng bố cục responsive hoặc khả năng truy cập cơ bản.

## 8. Skill: Chuẩn bị bản trình diễn

### Mục tiêu
Đảm bảo các luồng chính hoạt động và giới hạn được công bố rõ trước khi trình diễn.

### Checklist

- Đăng nhập, đăng xuất và OTP giả lập hoạt động theo phạm vi hiện tại.
- Dashboard, kho tài liệu, tìm kiếm, bộ lọc, phân trang và vừa mới xem hoạt động.
- Thêm, sửa, xóa, khôi phục tài liệu và quản lý tệp có trạng thái lỗi rõ ràng.
- Ghi chú độc lập và nhiều ghi chú trên một tài liệu được lưu đúng.
- Tùy chọn giao diện được ghi nhớ.
- Tóm tắt AI và gợi ý Knowledge Graph gọi qua lớp trung gian an toàn.
- Knowledge Graph chỉ đưa gợi ý thành liên kết khi người dùng chấp nhận.
- Dữ liệu cục bộ còn sau khi tải lại trang; lỗi lưu trữ được báo rõ.
- Ứng dụng chạy theo cách đã được dự án quy định; không tự thêm bước build.
- Tài liệu phản ánh đúng tính năng đã triển khai và các giới hạn còn tồn tại.