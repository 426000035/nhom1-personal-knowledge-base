# Product Backlog và kế hoạch thực hiện

## 1. Mục tiêu

Xây dựng trong một tuần bản MVP trình diễn của Personal Knowledge Base, giúp người dùng quản lý tài liệu và ghi chú cá nhân, tìm kiếm nội dung, xem chi tiết, theo dõi trạng thái đọc và khám phá liên kết tri thức.

Kế hoạch chia việc theo module độc lập, thống nhất hợp đồng dữ liệu trước khi phát triển, giới hạn phạm vi tệp để giảm xung đột và tích hợp liên tục.

## 2. Vai trò trong nhóm

| Vai trò | Trách nhiệm |
|---|---|
| Product Owner (người dùng/giảng viên) | Chốt yêu cầu, ưu tiên backlog và nghiệm thu các mốc. Các quyết định ngoài phạm vi đã chốt cần được xác nhận trước khi triển khai. |
| Tống Ngọc Minh Châu (M.Châu) — Giao diện và điều phối | Phụ trách khung ứng dụng, điều hướng, Dashboard, UI Kho/Chi tiết, tài khoản và Knowledge Graph; tích hợp giao diện, chuẩn bị luồng demo và mở PR 1/3. |
| Phan Thị Ngọc Duyên (N.Duyên) — Nhóm trưởng, dữ liệu và hoàn thiện | Điều phối tiến độ, chốt tích hợp; phụ trách hợp đồng dữ liệu, IndexedDB, CRUD, dịch vụ dùng chung, tích hợp Google Apps Script/gateway AI, kiểm thử lưu trữ; thực hiện PR 2 và PR 4, review PR 1/3. |
| Cả hai | Thống nhất hợp đồng dữ liệu, review thay đổi, kiểm thử luồng liên mô-đun và xử lý lỗi hồi quy. Mỗi phần có một người phụ trách chính; người còn lại review, tránh cùng sửa một tệp. N.Duyên là nhóm trưởng và điều phối quyết định trong phạm vi đã được Product Owner chốt. |

## 3. Quy ước phối hợp

- Thống nhất `data-contract.md` và các luồng trong `architecture.md` trước khi chia nhánh triển khai tính năng phụ thuộc dữ liệu.
- M.Châu không tự ghi dữ liệu trực tiếp từ giao diện hoặc tự thay đổi schema IndexedDB.
- N.Duyên không tự thay đổi layout, CSS chung hoặc hành vi màn hình nếu chưa thống nhất với M.Châu.
- Thay đổi schema, quan hệ dữ liệu, API hoặc phạm vi đã chốt phải được thống nhất và cập nhật tài liệu liên quan trước khi triển khai.
- Hai thành viên làm trên hai máy và bàn giao tuần tự qua đúng 4 Pull Request; không phát triển song song trên các nhánh cùng thay đổi một phần việc.
- Mỗi PR được review và squash-merge một lần; nhánh chính có đúng 4 commit tích hợp, mỗi commit tương ứng một PR.
- Chỉ tạo nhánh kế tiếp sau khi PR trước đã merge; cập nhật nhánh chính mới nhất trước khi tạo branch.

## 4. Kế hoạch theo ngày

Thời gian tính theo ngày kể từ lúc nhóm bắt đầu dự án; ngày lịch cụ thể chưa được cung cấp.

| PR / ngày | Người thực hiện và thứ tự | Phạm vi công việc | PR và kết quả bàn giao |
|---|---|---|---|
| **PR 1 — Ngày 1–2** | M.Châu thực hiện; N.Duyên review phạm vi, hợp đồng và PR. | Chốt màn hình/luồng/tiêu chí; dựng app shell, điều hướng responsive và Dashboard khung. Không triển khai schema hoặc ghi IndexedDB ở UI. | M.Châu tạo `feature/pkb-pr1-foundation`, hoàn tất tác vụ và mở PR 1 vào nhánh chính. N.Duyên review; squash-merge và xóa branch sau khi đạt. |
| **PR 2 — Ngày 3–4** | N.Duyên thực hiện sau khi PR 1 đã merge; M.Châu review API dịch vụ và PR. | Khởi tạo IndexedDB; CRUD tài liệu/URL/tag/thư mục; dịch vụ ghi chú, highlight, tiến độ, yêu thích và đọc; tích hợp ngoài chỉ khi endpoint sẵn sàng. Kiểm tra lỗi và dữ liệu sau tải lại. | N.Duyên cập nhật nhánh chính sau PR 1, tạo `feature/pkb-pr2-data`, hoàn tất và mở PR 2. M.Châu review; squash-merge và xóa branch sau khi đạt. |
| **PR 3 — Ngày 5–6** | M.Châu thực hiện sau khi PR 2 đã merge; N.Duyên review API và tích hợp. | Tích hợp Dashboard; hoàn thiện UI Kho/chi tiết/ghi chú/tài khoản/Graph; responsive và trạng thái loading/rỗng/lỗi. Tập trung hoàn thành chức năng đã duyệt, không mở rộng phạm vi. | M.Châu cập nhật nhánh chính sau PR 2, tạo `feature/pkb-pr3-integration`, hoàn tất và mở PR 3. N.Duyên review; squash-merge và xóa branch sau khi đạt. |
| **PR 4 — Ngày 7 và thời gian chốt** | N.Duyên thực hiện với vai trò nhóm trưởng; M.Châu review và xác nhận giao diện/luồng. | Tích hợp bản cuối; rà soát tiêu chí đã duyệt; sửa lỗi hồi quy, hoàn tất chức năng trong backlog còn thiếu, kiểm tra dữ liệu/lỗi/bảo mật cấu hình, cập nhật tài liệu và chuẩn bị nghiệm thu. Không thêm tính năng ngoài phạm vi nếu chưa được Product Owner duyệt. | N.Duyên tạo `feature/pkb-pr4-finalization` từ nhánh chính sau PR 3, mở PR 4 cuối cùng. M.Châu review; squash-merge sau khi đạt. Đây là PR cuối để chốt ứng dụng. |

Các PR được làm tuần tự: PR 2 bắt đầu sau khi PR 1 merge; PR 3 bắt đầu sau khi PR 2 merge; PR 4 bắt đầu sau khi PR 3 merge. Mỗi PR có thể cập nhật nhiều lần trong quá trình review nhưng giữ nguyên PR, không mở PR thay thế. Nếu một dịch vụ bị chặn do thiếu endpoint/gateway, ghi rõ trạng thái; không giả lập thành công. N.Duyên điều phối PR 4 nhưng không tự phê duyệt yêu cầu mới ngoài backlog.

## 5. Backlog theo module

| ID | Công việc | Phụ trách | Hỗ trợ AI phù hợp | Ưu tiên | Tiêu chí hoàn thành |
|---|---|---|---|---|---|
| PB-01 | Chốt màn hình, luồng người dùng và tiêu chí MVP | M.Châu + N.Duyên | Tóm tắt user stories, phát hiện yêu cầu mâu thuẫn | Cao | Danh sách màn hình, luồng và tiêu chí được thống nhất trước khi phát triển module phụ thuộc. |
| PB-02 | Chốt hợp đồng dữ liệu và giao diện dịch vụ | N.Duyên; M.Châu review | Đề xuất schema và kiểm tra tính nhất quán với user stories | Cao | Các module dùng chung tên trường, quan hệ và quy tắc lưu trữ theo `data-contract.md`. |
| PB-03 | Dựng khung ứng dụng, điều hướng và responsive layout | M.Châu | Tạo khung HTML/CSS theo cấu trúc hiện có | Cao | Có thể mở ứng dụng, điều hướng đến các khu vực chính và dùng được ở kích thước màn hình hỗ trợ. |
| PB-04 | Khởi tạo IndexedDB và dịch vụ dữ liệu nền | N.Duyên | Soạn CRUD theo hợp đồng; đề xuất ca lỗi lưu trữ | Cao | Dữ liệu mẫu có thể tạo, đọc và đọc lại sau khi tải trang; lỗi lưu không bị báo thành công. |
| PB-05 | Dashboard: mới thêm, vừa mới xem, thống kê, truy cập nhanh | M.Châu; N.Duyên cung cấp dữ liệu | Tạo UI và kiểm tra cách tính thống kê theo tiêu chí | Cao | Dashboard hiển thị dữ liệu hiện có; tài liệu đã xóa không tính trong kho hoạt động. |
| PB-06 | Kho tài liệu: Card/List, tìm kiếm, lọc, sắp xếp, phân trang | M.Châu giao diện; N.Duyên dịch vụ lọc nếu cần | Viết hàm lọc/sắp xếp thuần và gợi ý ca kiểm thử | Cao | Không tải lại trang; hỗ trợ 10/20/50/all; lọc và tìm kiếm kết hợp chính xác. |
| PB-07 | CRUD tài liệu, URL, tag và thư mục | N.Duyên; M.Châu tích hợp giao diện | Tạo kiểm tra dữ liệu và kiểm thử tham chiếu | Cao | Thêm/sửa/xóa hoạt động; dữ liệu hợp lệ; thao tác nguy cơ mất dữ liệu có xác nhận phù hợp. |
| PB-08 | Trang chi tiết và xem trước định dạng | M.Châu; N.Duyên cung cấp dữ liệu tệp | Hỗ trợ bộ chọn renderer và trạng thái không hỗ trợ | Cao | Trang chi tiết nhận ID, hiển thị đúng thông tin và báo rõ khi không thể xem trước. |
| PB-09 | Ghi chú độc lập, nhiều ghi chú trên một tài liệu, highlight | N.Duyên nghiệp vụ; M.Châu giao diện | Đề xuất ca kiểm thử quan hệ và thao tác CRUD | Cao | Tạo/sửa/xóa từng ghi chú; ghi chú liên kết đúng tài liệu và không lẫn nội dung gốc. |
| PB-10 | Yêu thích, trạng thái đọc, tiến độ và tùy chọn giao diện | N.Duyên dữ liệu; M.Châu giao diện | Kiểm tra trạng thái và persistence sau tải lại | Trung bình | Trạng thái hiển thị nhất quán và được lưu sau khi tải lại. |
| PB-11 | Đăng ký, đăng nhập, Auth Guard, OTP giả lập, đăng xuất | M.Châu giao diện; N.Duyên tích hợp Apps Script/Sheets | Hỗ trợ kiểm tra validation và các nhánh lỗi | Trung bình/cao | Luồng demo hoạt động nếu endpoint sẵn có; OTP được thể hiện rõ là giả lập; lỗi tài khoản được báo; không tuyên bố rằng đăng nhập phân vùng hoặc bảo vệ nội dung IndexedDB. |
| PB-12 | Tóm tắt AI qua gateway và lưu thành ghi chú theo yêu cầu | N.Duyên gateway; M.Châu giao diện | Hỗ trợ định dạng prompt và kiểm thử phản hồi | Trung bình; phụ thuộc dịch vụ | Yêu cầu qua gateway; không lộ khóa trong frontend; chỉ lưu ghi chú khi người dùng chọn và lưu thành công. |
| PB-13 | Knowledge Graph bằng vis-network, gợi ý AI và quyết định người dùng | M.Châu hiển thị; N.Duyên dữ liệu/dịch vụ | Hỗ trợ tạo gợi ý chủ đề và rà soát định dạng phản hồi | Trung bình; phụ thuộc dịch vụ | Node/quan hệ đúng; gợi ý tách khỏi liên kết chính thức; chỉ chấp nhận mới tạo liên kết. |
| PB-14 | Tích hợp, kiểm thử hồi quy, sửa lỗi và chuẩn bị demo | N.Duyên nhóm trưởng; M.Châu phối hợp | Rà soát checklist, đề xuất ca kiểm thử | Cao | Cả bốn PR đã merge; lỗi/chức năng còn thiếu trong phạm vi đã duyệt được xử lý hoặc ghi rõ lý do; demo và giới hạn được công bố. |

## 6. Kế hoạch Pull Request và bàn giao Git

Nhóm làm trên hai máy qua **đúng 4 PR tuần tự**. Mỗi PR được **Squash and merge**, tạo đúng một commit tích hợp trên nhánh chính; tổng cộng bốn commit tích hợp trên nhánh chính.

| PR | Thời điểm | Người phụ trách | Nhánh | Nội dung |
|---|---|---|---|---|
| **PR 1** | Cuối Ngày 2 | M.Châu; N.Duyên review | `feature/pkb-pr1-foundation` | Phạm vi đã thống nhất, app shell, điều hướng responsive và Dashboard khung. |
| **PR 2** | Cuối Ngày 4 | N.Duyên; M.Châu review | `feature/pkb-pr2-data` | IndexedDB, CRUD, nghiệp vụ và dịch vụ dữ liệu đã kiểm thử. |
| **PR 3** | Cuối Ngày 6 | M.Châu; N.Duyên review | `feature/pkb-pr3-integration` | UI Kho/chi tiết, tích hợp Dashboard, ghi chú, tài khoản demo và Graph. |
| **PR 4** | Cuối Ngày 7 / chốt | N.Duyên (nhóm trưởng); M.Châu review | `feature/pkb-pr4-finalization` | Rà soát tiêu chí đã duyệt, sửa lỗi/chức năng còn thiếu trong phạm vi, hồi quy và nghiệm thu demo. |

Quy trình bắt buộc:

1. Tác giả cập nhật nhánh chính sau PR trước, rồi tạo feature branch mới từ nhánh chính mới nhất.
2. Tác giả làm các tác vụ thuộc PR, kiểm tra diff, chạy xác minh phù hợp, tạo PR vào nhánh chính và gán người còn lại review.
3. Reviewer đọc mô tả/Files changed, kiểm tra tiêu chí nghiệm thu, yêu cầu sửa trong cùng PR nếu cần; không tạo PR thay thế.
4. Chỉ squash-merge sau khi được duyệt; xóa feature branch sau merge.
5. Thành viên kế tiếp fetch/pull nhánh chính đã cập nhật trước khi tạo branch/PR của mình.

Mỗi PR có thể có nhiều commit ở feature branch để hỗ trợ review; squash merge bảo đảm nhánh chính nhận một commit cho mỗi PR. Thực hiện đúng bốn PR theo lịch trên; không tạo PR thứ năm, không tạo merge commit thường, không force-push và không commit khóa API, token, mật khẩu hoặc dữ liệu cá nhân thật. Nếu PR chưa được merge, chờ hoặc lùi lịch; không tạo PR tiếp theo từ nhánh chính cũ.

## 7. Rủi ro, phụ thuộc và ưu tiên khi thiếu thời gian

- **API Google Apps Script/Sheets:** endpoint, quyền truy cập và cấu trúc request/response cần có sớm. Nếu chưa sẵn sàng, đánh dấu PB-11 bị chặn; không giả lập rồi tuyên bố đã tích hợp thật.
- **Phân tách dữ liệu tài khoản:** không thuộc phạm vi MVP. Nội dung lưu trong IndexedDB được dùng chung trong cùng hồ sơ trình duyệt; đăng nhập demo và Auth Guard phía client không phải ranh giới bảo mật.
- **API AI thật:** cần nhà cung cấp và gateway phía máy chủ để bảo vệ thông tin xác thực. Nếu gateway chưa có, đánh dấu PB-12/PB-13 bị chặn hoặc chỉ hoàn thành giao diện theo phạm vi được Product Owner chấp thuận; không gọi API có khóa bí mật trực tiếp từ trình duyệt.
- **Phạm vi một tuần:** ưu tiên nền tảng IndexedDB, quản lý tài liệu, ghi chú, tìm kiếm/lọc, chi tiết và demo ổn định. Các trình xem định dạng phức tạp có thể được giới hạn theo thời gian, nhưng phải ghi rõ định dạng nào chưa hoàn thành.
- **Thứ tự giảm phạm vi:** trước hết hoàn tất luồng dữ liệu cốt lõi; sau đó hoàn thiện tích hợp ngoài; cuối cùng bổ sung chi tiết trình xem và tương tác graph nâng cao. Không âm thầm bỏ tiêu chí đã chốt — cần báo Product Owner và ghi lại quyết định.

## 8. Tiêu chí nghiệm thu cuối tuần

- Mở ứng dụng và điều hướng được giữa các màn hình MVP.
- Tạo, xem, cập nhật và xóa nội dung theo luồng đã triển khai.
- Tìm kiếm, lọc, sắp xếp và phân trang 10/20/50/all cho kết quả chính xác.
- Dữ liệu nội dung lưu trong IndexedDB vẫn còn sau khi tải lại trang.
- Nhiều ghi chú có thể gắn với cùng một tài liệu; trạng thái yêu thích/đọc hiển thị phù hợp.
- Có thông báo rõ cho dữ liệu rỗng, đầu vào sai, thao tác thất bại và loại tệp không hỗ trợ.
- Knowledge Graph không biến gợi ý AI thành liên kết chính thức nếu chưa có chấp thuận của người dùng.
- Không lộ thông tin xác thực API trong mã phía trình duyệt.
- Có đúng 4 PR được review và squash-merge; nhánh chính có đúng 4 commit tích hợp tương ứng.
- Demo và tài liệu nêu rõ chức năng hoàn thành, chưa hoàn thành và dịch vụ ngoài còn phụ thuộc.