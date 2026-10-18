# Personal Knowledge Base

Ứng dụng web phía trình duyệt để quản lý tài liệu, đường dẫn và ghi chú cá nhân; hỗ trợ tìm kiếm, phân loại, theo dõi tiến độ đọc và khám phá liên kết tri thức.

## Trạng thái hiện tại

Kho hiện có tài liệu đặc tả; `index.html` đang rỗng nên chưa có ứng dụng chạy được hoặc lệnh chạy để hướng dẫn. Khi phần giao diện được triển khai, cập nhật mục này bằng cách chạy đã kiểm chứng. Dự án được định hướng dùng HTML, CSS và JavaScript thuần, không cần bước build.

Các tính năng dự kiến dùng Google Apps Script hoặc API AI cần endpoint tương ứng được cấu hình riêng. Không đưa khóa bí mật vào mã chạy phía trình duyệt.

## Giới hạn bản demo

- Nội dung tài liệu được lưu cục bộ trong IndexedDB của trình duyệt; không tự đồng bộ hoặc sao lưu lên đám mây.
- Đăng nhập Google Apps Script/Google Sheets là luồng demo và không phân vùng nội dung IndexedDB theo tài khoản. Người dùng chung hồ sơ trình duyệt có thể truy cập cùng dữ liệu cục bộ.
- Khôi phục mật khẩu dùng OTP giả lập, không phải xác minh danh tính an toàn.
- Tóm tắt AI và gợi ý AI cần API thật thông qua lớp trung gian phía máy chủ; không dùng khóa API trong frontend.

## Tài liệu dự án

- [User stories](./user-stories.md): yêu cầu người dùng và tiêu chí chấp nhận.
- [Architecture](./architecture.md): màn hình, luồng và quyết định kỹ thuật.
- [Data contract](./data-contract.md): mô hình dữ liệu, lưu trữ và quy tắc nghiệp vụ.
- [Product backlog](./product-backlog.md): ưu tiên, phân công và kế hoạch.
- [Prompt kế hoạch 7 ngày](./prompt-ke-hoach-7-ngay.md): prompt theo tác vụ và hướng dẫn tạo/review bốn PR tuần tự trên hai máy; PR cuối do nhóm trưởng Phan Thị Ngọc Duyên (N.Duyên) phụ trách chốt ứng dụng.
- [AI instructions](./AI_INSTRUCTIONS.md): điểm vào hướng dẫn trợ lý AI.
- [AI agent guidelines](./.ai/AGENTS.md): quy tắc làm việc trong dự án.
- [AI workflows](./.ai/SKILLS.md): quy trình tính năng, dữ liệu và kiểm thử.
- [Changelog](./CHANGELOG.md): lịch sử thay đổi tài liệu và sản phẩm.
