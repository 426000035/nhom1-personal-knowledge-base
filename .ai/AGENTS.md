# AGENTS.md

## 1. Tổng quan dự án

Tên dự án: Personal Knowledge Base.

Loại dự án: Ứng dụng web quản lý tài liệu và tri thức cá nhân, chạy trên trình duyệt.

Ứng dụng hỗ trợ:
- Quản lý tài liệu, URL và tệp tải lên.
- Sắp xếp nội dung bằng thư mục và tag.
- Tạo ghi chú độc lập và nhiều ghi chú liên kết với cùng một tài liệu.
- Tạo highlight liên kết với ghi chú và tài liệu.
- Theo dõi trạng thái đọc và tiến độ đọc.
- Tìm kiếm, lọc, sắp xếp và phân trang tài liệu.
- Hiển thị tài liệu mới thêm và tài liệu vừa mới xem.
- Xem các định dạng tài liệu được hỗ trợ trên trình duyệt.
- Quản lý yêu thích, thùng rác và khôi phục.
- Cung cấp AI Assistant mô phỏng bằng kịch bản cục bộ.
- Gọi API AI thật qua lớp trung gian phía máy chủ để tóm tắt tài liệu và gợi ý liên kết theo chủ đề cho Knowledge Graph.
- Hiển thị Knowledge Graph bằng vis-network.

## 2. Tài liệu và nguồn yêu cầu

Trước khi thực hiện yêu cầu, đọc các tài liệu liên quan:

- `../user-stories.md`: yêu cầu người dùng và tiêu chí chấp nhận.
- `../architecture.md`: màn hình, luồng chức năng, quyết định kỹ thuật và các điểm chưa chốt.
- `../data-contract.md`: mô hình dữ liệu, quan hệ, quy tắc lưu trữ và nghiệp vụ.
- `SKILLS.md`: quy trình phát triển, tích hợp và kiểm thử có thể tái sử dụng.

Thứ tự ưu tiên khi áp dụng yêu cầu:

1. Quyết định mới nhất của người dùng cho tác vụ hiện tại.
2. `architecture.md` đối với kiến trúc và chức năng đã chốt.
3. `data-contract.md` đối với mô hình dữ liệu và quy tắc lưu trữ.
4. `user-stories.md` đối với chi tiết tính năng và tiêu chí chấp nhận.
5. Mã hiện có, nếu không mâu thuẫn với các nguồn trên.

Nếu yêu cầu mới mâu thuẫn với quyết định đã chốt hoặc đòi hỏi thay đổi phạm vi, hợp đồng dữ liệu, ranh giới bảo mật hay kiến trúc, hãy nêu rõ mâu thuẫn và hỏi người dùng trước khi thay đổi. Không tự ý diễn giải lại yêu cầu.

## 3. Công nghệ và giới hạn môi trường

- Sử dụng HTML5, CSS3 và JavaScript thuần.
- Ứng dụng phải chạy trực tiếp trên trình duyệt, không cần bước build.
- Không tự ý thêm framework hoặc công cụ build nếu chưa được người dùng chấp thuận.
- Dùng localStorage cho tùy chọn nhỏ và phiên đăng nhập theo kiến trúc.
- Dùng IndexedDB cho nội dung ứng dụng, dữ liệu có cấu trúc, quan hệ và tệp tải lên.
- Không lưu tệp lớn hoặc dữ liệu nhị phân trong localStorage.
- Dùng Google Apps Script và Google Sheets cho các thao tác tài khoản theo kiến trúc.
- Đăng nhập/khôi phục tài khoản là luồng demo; nội dung IndexedDB không phân vùng theo tài khoản. Không mô tả Auth Guard phía client là kiểm soát truy cập an toàn.
- Gọi API AI thật thông qua lớp trung gian phía máy chủ. Không để lộ khóa API hoặc thông tin bí mật trong mã trình duyệt.
- Dùng vis-network để hiển thị Knowledge Graph theo quyết định đã chốt.
- Giới hạn phụ thuộc mới trong phạm vi đã duyệt và ghi nhận chúng trong tài liệu phù hợp.

## 4. Phạm vi dự án

Triển khai và duy trì các chức năng đã được duyệt trong `architecture.md` và `user-stories.md`, bao gồm:

- Đăng ký, đăng nhập, đăng xuất và khôi phục mật khẩu bằng OTP giả lập.
- Nội dung IndexedDB dùng chung trong cùng hồ sơ trình duyệt, không có cách ly tài khoản.
- Dashboard có tài liệu mới thêm, tài liệu vừa mới xem, thống kê và lối truy cập nhanh.
- Kho tài liệu có dạng Card/List, tìm kiếm, bộ lọc, sắp xếp và các lựa chọn phân trang 10, 20, 50 hoặc tất cả.
- Quản lý tài liệu, URL, tệp, thư mục và tag; định dạng tệp được phép theo `data-contract.md`.
- Chi tiết tài liệu và trình xem các định dạng được hỗ trợ.
- Ghi chú độc lập và nhiều ghi chú liên kết với cùng một tài liệu.
- Highlight, yêu thích, trạng thái đọc và tiến độ đọc.
- Tùy chọn, thùng rác, khôi phục và xác nhận trước thao tác có thể gây mất dữ liệu.
- AI Assistant mô phỏng cục bộ.
- Tóm tắt tài liệu bằng API AI thật qua lớp trung gian phía máy chủ.
- Knowledge Graph có quan hệ đã xác nhận và gợi ý AI cần người dùng chấp thuận.

Không bổ sung các chức năng chưa được duyệt như tìm kiếm ngữ nghĩa, tự động chấp nhận gợi ý AI, đồng bộ dữ liệu cá nhân lên đám mây hoặc để AI tự ý sửa/xóa dữ liệu người dùng.

## 5. Vai trò của các tác nhân AI

AI chỉ đảm nhận vai trò phù hợp với tác vụ được giao. Các vai trò dưới đây mô tả trách nhiệm, không có nghĩa là tự khởi chạy nhiều agent, sử dụng công cụ khác hoặc mở rộng phạm vi.

### 5.1 Điều phối viên / Kỹ sư phụ trách

- Làm rõ kết quả cần đạt và tiêu chí chấp nhận.
- Đọc hướng dẫn dự án và kiểm tra phần triển khai hiện có trước khi đề xuất hoặc thay đổi.
- Xác định màn hình, mô-đun, dịch vụ, dữ liệu và tài liệu bị ảnh hưởng.
- Giới hạn thay đổi trong phạm vi được duyệt.
- Hỏi người dùng khi có điểm chưa rõ có ảnh hưởng đáng kể hoặc khi cần đổi phạm vi đã chốt.
- Không giao việc hoặc khởi chạy agent khác trừ khi người dùng yêu cầu rõ ràng.

### 5.2 Chuyên viên phân tích yêu cầu và sản phẩm

- Chuyển user stories thành màn hình, luồng thao tác và tiêu chí chấp nhận có thể kiểm tra.
- Phân biệt yêu cầu đã chốt với quyết định còn bỏ ngỏ.
- Cập nhật các quyết định mới nhất của người dùng vào tài liệu phù hợp.
- Không tự đặt ra hành vi, cam kết bảo mật hoặc quy tắc nghiệp vụ chưa được xác định.

### 5.3 Kỹ sư giao diện và trải nghiệm người dùng

- Xây dựng HTML có ngữ nghĩa, dễ truy cập và giao diện responsive bằng HTML, CSS, JavaScript thuần.
- Tuân theo sơ đồ màn hình và điều hướng trong `architecture.md`.
- Cung cấp trạng thái đang tải, rỗng, thành công và lỗi rõ ràng.
- Tách xử lý giao diện khỏi dịch vụ dữ liệu và tích hợp dùng chung.
- Giữ khả năng thao tác bằng bàn phím và hành vi responsive hiện có.

### 5.4 Kỹ sư dữ liệu và IndexedDB

- Tuân theo `data-contract.md` về entity, tham chiếu và quy tắc xóa.
- Dùng dịch vụ dữ liệu dùng chung thay vì để từng màn hình tự triển khai lưu trữ riêng.
- Giữ dữ liệu và tham chiếu nhất quán khi tạo, cập nhật, xóa, khôi phục hoặc liên kết.
- Báo lỗi rõ ràng khi giao dịch thất bại, bộ nhớ không khả dụng hoặc hết dung lượng, hay không tìm thấy bản ghi.
- Chỉ thông báo lưu thành công khi giao dịch IndexedDB hoàn tất.
- Lập kế hoạch và kiểm tra chuyển đổi dữ liệu trước khi đổi schema đã lưu.

### 5.5 Kỹ sư tích hợp tài khoản

- Triển khai yêu cầu tài khoản thông qua tích hợp Google Apps Script / Google Sheets đã được duyệt.
- Triển khai khôi phục mật khẩu bằng OTP giả lập và nêu rõ đây là cơ chế mô phỏng.
- Kiểm tra dữ liệu đầu vào và hiển thị rõ kết quả thành công hoặc thất bại.
- Không mô tả OTP giả lập như một phương thức xác minh danh tính an toàn.
- Giữ nguyên hành vi phiên đăng nhập và đăng xuất đã được duyệt.
- Không tự ý thêm nhà cung cấp tài khoản hoặc backend khác.

### 5.6 Kỹ sư tích hợp AI

- Triển khai tóm tắt tài liệu và gợi ý liên kết tri thức theo chủ đề thông qua lớp trung gian AI phía máy chủ.
- Chỉ gửi lượng nội dung và metadata tối thiểu cần thiết cho tác vụ AI được yêu cầu.
- Giữ khóa và thông tin xác thực ở phía máy chủ; không đưa chúng vào JavaScript trình duyệt, bộ nhớ trình duyệt hoặc log.
- Kiểm tra và xử lý an toàn phản hồi AI trước khi hiển thị hoặc lưu.
- Hiển thị trạng thái đang xử lý, lỗi và khả năng thử lại khi phù hợp.
- Chỉ lưu bản tóm tắt thành ghi chú khi người dùng yêu cầu và thao tác lưu thành công.
- Không để AI tự tạo, sửa, xóa hoặc công bố dữ liệu nếu người dùng chưa chủ động yêu cầu.
- Không trình bày nội dung AI tạo ra như sự thật đã được xác minh.

### 5.7 Kỹ sư Knowledge Graph

- Hiển thị các nút tài liệu, ghi chú và tag bằng vis-network.
- Tạo các cạnh đã xác nhận từ dữ liệu và quan hệ được định nghĩa trong `data-contract.md`.
- Hiển thị riêng gợi ý AI và liên kết đã xác nhận.
- Chỉ tạo liên kết đã xác nhận sau khi người dùng chấp thuận rõ ràng gợi ý AI.
- Không tạo cạnh trùng cho quan hệ vốn đã suy ra được từ tag hoặc liên kết ghi chú–tài liệu.
- Hỗ trợ các thao tác đã duyệt như phóng to, kéo thả, lọc và mở entity khi chọn nút.
- Xử lý entity không tồn tại, liên kết trùng, liên kết tự tham chiếu, đồ thị rỗng và lỗi lưu.

### 5.8 Kỹ sư kiểm thử và độ tin cậy

- Tạo kiểm thử dựa trên tiêu chí chấp nhận và quy tắc trong hợp đồng dữ liệu.
- Kiểm tra luồng thành công chính, dữ liệu rỗng, đầu vào không hợp lệ, tham chiếu không tồn tại, lỗi lưu trữ và lỗi mạng.
- Xác minh dữ liệu còn sau khi tải lại trang.
- Kiểm tra các luồng liên quan để phát hiện hồi quy sau mỗi thay đổi.
- Kiểm tra phản hồi lỗi AI và bảo đảm gợi ý liên kết chưa được xác nhận cho đến khi người dùng chấp thuận.
- Báo cáo kiểm tra nào đã chạy và nêu rõ giới hạn còn lại.

### 5.9 Người duy trì tài liệu

- Chỉ cập nhật tài liệu bị ảnh hưởng trực tiếp bởi thay đổi đã được duyệt.
- Giữ cho kiến trúc, user stories, hợp đồng dữ liệu và hành vi triển khai nhất quán.
- Ghi rõ quyết định chưa xác định là `chưa chốt`.
- Không khẳng định một tính năng, thư viện, bài kiểm thử hoặc thuộc tính bảo mật tồn tại nếu chưa kiểm chứng.

## 6. Quy tắc kỹ thuật chung

- Thay đổi chính xác, đầy đủ và nằm trong phạm vi yêu cầu.
- Kiểm tra mã hiện có và tái sử dụng helper/dịch vụ đã được thiết lập.
- Tách HTML, CSS, xử lý giao diện, nghiệp vụ và lưu trữ khi phù hợp.
- Tránh logic trùng lặp, trạng thái toàn cục, trừu tượng hóa và phụ thuộc không cần thiết.
- Kiểm tra đầu vào và tham chiếu trước khi lưu.
- Hiển thị lỗi rõ ràng; không âm thầm bỏ qua ngoại lệ hoặc trả về kết quả giả thành công.
- Yêu cầu xác nhận trước thao tác phá hủy dữ liệu và giữ nguyên dữ liệu nếu người dùng hủy.
- Không ghi đè chức năng hiện tại khi chưa kiểm tra nơi sử dụng và phụ thuộc của nó.
- Giữ nội dung tài liệu cá nhân trong IndexedDB, trừ khi người dùng chấp thuận rõ cách lưu trữ khác.
- Không gửi nội dung cá nhân tới dịch vụ AI ngoài phần cần thiết cho thao tác AI do người dùng yêu cầu.
- Không đưa thông tin xác thực, bí mật hoặc dữ liệu người dùng thật vào mã nguồn.

## 7. Quy trình thay đổi

Trước khi triển khai:

1. Xác định kết quả người dùng mong muốn và tiêu chí chấp nhận.
2. Kiểm tra các tệp liên quan và phần triển khai hiện có.
3. Đọc các phần phù hợp trong kiến trúc, hợp đồng dữ liệu và user stories.
4. Xác định mô-đun, dịch vụ, bản ghi lưu trữ và tài liệu bị ảnh hưởng.
5. Kiểm tra xung đột với các quyết định đã chốt.
6. Nếu còn quyết định quan trọng chưa rõ, hỏi người dùng trước khi lựa chọn.

Trong khi triển khai:

1. Thực hiện thay đổi nhỏ nhất nhưng đầy đủ để đáp ứng yêu cầu.
2. Nếu cần đổi mô hình đã lưu hoặc quy tắc nghiệp vụ, cập nhật hợp đồng dữ liệu trước.
3. Giữ nguyên dữ liệu người dùng và hành vi hiện có ngoài phạm vi thay đổi.
4. Xử lý kiểm tra đầu vào, trạng thái đang tải, rỗng, thành công và lỗi.

Trước khi hoàn tất:

1. Chạy lệnh kiểm thử, lint hoặc kiểm tra hiện có nhỏ nhất phù hợp.
2. Kiểm tra hồi quy các luồng liên quan.
3. Rà soát diff cuối để loại bỏ thay đổi ngoài phạm vi.
4. Cập nhật tài liệu liên quan trực tiếp.
5. Tóm tắt tệp đã thay đổi, kiểm tra đã chạy và giới hạn còn lại.

## 8. Tiêu chí hoàn thành

Một tác vụ hoàn thành khi:

- Hành vi được yêu cầu đáp ứng tiêu chí chấp nhận.
- Dữ liệu tuân theo `data-contract.md`.
- Lỗi và đầu vào không hợp lệ được xử lý, thông báo rõ ràng.
- Chức năng liên quan hiện có vẫn hoạt động.
- Các kiểm tra phù hợp đã được chạy và kết quả được báo cáo.
- Tài liệu phản ánh chính xác hành vi đã được duyệt.