# Product Backlog và kế hoạch thực hiện

## 1. Mục tiêu

Xây dựng trong một tuần bản MVP trình diễn của Personal Knowledge Base, giúp người dùng quản lý tài liệu và ghi chú cá nhân, tìm kiếm nội dung, xem chi tiết, theo dõi trạng thái đọc và khám phá liên kết tri thức.

Kế hoạch chia việc theo module độc lập, thống nhất hợp đồng dữ liệu trước khi phát triển, giới hạn phạm vi tệp để giảm xung đột và tích hợp liên tục.

## 2. Vai trò trong nhóm

| Vai trò | Trách nhiệm |
|---|---|
| Product Owner (người dùng/giảng viên) | Chốt yêu cầu, ưu tiên backlog và nghiệm thu các mốc. Các quyết định ngoài phạm vi đã chốt cần được xác nhận trước khi triển khai. |
| Thành viên A — Giao diện và điều phối | Theo dõi tiến độ; phụ trách khung ứng dụng, điều hướng, giao diện Dashboard, Kho tài liệu, Chi tiết, tài khoản và Knowledge Graph; chuẩn bị luồng demo. |
| Thành viên B — Dữ liệu và dịch vụ | Phụ trách hợp đồng dữ liệu, IndexedDB, nghiệp vụ CRUD, dịch vụ dùng chung, tích hợp Google Apps Script và lớp trung gian AI; kiểm thử lưu trữ và tích hợp. |
| Cả hai | Thống nhất hợp đồng dữ liệu, review thay đổi của nhau, kiểm thử luồng liên mô-đun và xử lý lỗi hồi quy. Mỗi phần có một người phụ trách chính; người còn lại review, tránh cùng sửa một tệp. |

## 3. Quy ước phối hợp

- Thống nhất `data-contract.md` và các luồng trong `architecture.md` trước khi chia nhánh triển khai tính năng phụ thuộc dữ liệu.
- Thành viên A không tự ghi dữ liệu trực tiếp từ giao diện hoặc tự thay đổi schema IndexedDB.
- Thành viên B không tự thay đổi layout, CSS chung hoặc hành vi màn hình nếu chưa thống nhất với A.
- Thay đổi schema, quan hệ dữ liệu, API hoặc phạm vi đã chốt phải được thống nhất và cập nhật tài liệu liên quan trước khi triển khai.
- Hai thành viên làm trên hai máy và bàn giao tuần tự qua Git; không phát triển song song trên các nhánh cùng thay đổi một phần việc.
- Toàn dự án có đúng 3 commit, mỗi commit là một mốc bàn giao đã review và được push để thành viên kế tiếp lấy về.
- Người nhận phải fetch/pull commit trước khi tạo nhánh làm tiếp; nhánh mới phải được tạo từ commit bàn giao gần nhất để lịch sử tuyến tính.
- Tên thành viên đang dùng A/B làm ký hiệu phân công; thay bằng tên thật của nhóm trước khi nộp nếu cần.

## 4. Kế hoạch theo ngày

Thời gian tính theo ngày kể từ lúc nhóm bắt đầu dự án; ngày lịch cụ thể chưa được cung cấp.

| Chặng / ngày | Người thực hiện và thứ tự | Phạm vi công việc | Git và kết quả bàn giao |
|---|---|---|---|
| **Chặng 1 — Ngày 1–2** | A thực hiện; B review từ xa các quyết định phạm vi và hợp đồng dữ liệu trước khi chốt. | Chốt màn hình, luồng, tiêu chí MVP; dựng app shell, điều hướng responsive và Dashboard khung với trạng thái rỗng/dữ liệu mẫu. A không tự triển khai schema hoặc ghi IndexedDB. | A tạo nhánh `work/pkb-01-foundation` từ nhánh chính, tạo **commit 1** gồm tài liệu đã review và khung giao diện, rồi push. B fetch/pull nhánh này và xác nhận SHA, trạng thái mã trước khi bắt đầu chặng 2. |
| **Chặng 2 — Ngày 3–5** | B thực hiện sau khi lấy commit 1; A review hợp đồng dịch vụ và kiểm tra tích hợp qua trao đổi, không push thay đổi riêng. | Khởi tạo IndexedDB; CRUD tài liệu/URL/tag/thư mục; dịch vụ tìm kiếm/lọc nếu cần; ghi chú, highlight, tiến độ, yêu thích; dịch vụ tài khoản/AI/Graph nếu endpoint sẵn sàng. Kiểm tra lỗi và dữ liệu sau tải lại. | B tạo nhánh mới `work/pkb-02-data` từ `work/pkb-01-foundation`, tạo **commit 2** cho lớp dữ liệu/dịch vụ đã hoàn tất, rồi push. A fetch/pull nhánh này, kiểm tra SHA và chạy smoke test trước chặng 3. |
| **Chặng 3 — Ngày 5–7** | A thực hiện sau khi lấy commit 2; B review và chạy kiểm thử dữ liệu trước khi chốt. | Tích hợp Dashboard với dịch vụ; hoàn thiện UI Kho, chi tiết, ghi chú, tài khoản demo và Knowledge Graph; responsive, loading/rỗng/lỗi; hồi quy, hướng dẫn demo và giới hạn dịch vụ chưa có. | A tạo nhánh mới `work/pkb-03-integration` từ `work/pkb-02-data`, tạo **commit 3** cuối cùng và push. B fetch/pull, nghiệm thu. Nhánh này là nhánh bàn giao cuối. Không push lần thứ tư để cập nhật nhánh chính; nếu cần, chỉ tích hợp bằng fast-forward theo chính sách repo, không tạo merge commit. |

Ngày 5 là điểm chuyển giao tuần tự: B hoàn tất và push chặng 2 trước; sau đó A mới kéo nhánh mới nhất và bắt đầu tích hợp chặng 3. Nếu một phần dịch vụ bị chặn do thiếu endpoint/gateway, ghi rõ trạng thái; không giả lập thành công để kịp mốc.

## 5. Backlog theo module

| ID | Công việc | Phụ trách | Hỗ trợ AI phù hợp | Ưu tiên | Tiêu chí hoàn thành |
|---|---|---|---|---|---|
| PB-01 | Chốt màn hình, luồng người dùng và tiêu chí MVP | A + B | Tóm tắt user stories, phát hiện yêu cầu mâu thuẫn | Cao | Danh sách màn hình, luồng và tiêu chí được thống nhất trước khi phát triển module phụ thuộc. |
| PB-02 | Chốt hợp đồng dữ liệu và giao diện dịch vụ | B; A review | Đề xuất schema và kiểm tra tính nhất quán với user stories | Cao | Các module dùng chung tên trường, quan hệ và quy tắc lưu trữ theo `data-contract.md`. |
| PB-03 | Dựng khung ứng dụng, điều hướng và responsive layout | A | Tạo khung HTML/CSS theo cấu trúc hiện có | Cao | Có thể mở ứng dụng, điều hướng đến các khu vực chính và dùng được ở kích thước màn hình hỗ trợ. |
| PB-04 | Khởi tạo IndexedDB và dịch vụ dữ liệu nền | B | Soạn CRUD theo hợp đồng; đề xuất ca lỗi lưu trữ | Cao | Dữ liệu mẫu có thể tạo, đọc và đọc lại sau khi tải trang; lỗi lưu không bị báo thành công. |
| PB-05 | Dashboard: mới thêm, vừa mới xem, thống kê, truy cập nhanh | A; B cung cấp dữ liệu | Tạo UI và kiểm tra cách tính thống kê theo tiêu chí | Cao | Dashboard hiển thị dữ liệu hiện có; tài liệu đã xóa không tính trong kho hoạt động. |
| PB-06 | Kho tài liệu: Card/List, tìm kiếm, lọc, sắp xếp, phân trang | A giao diện; B dịch vụ lọc nếu cần | Viết hàm lọc/sắp xếp thuần và gợi ý ca kiểm thử | Cao | Không tải lại trang; hỗ trợ 10/20/50/all; lọc và tìm kiếm kết hợp chính xác. |
| PB-07 | CRUD tài liệu, URL, tag và thư mục | B; A tích hợp giao diện | Tạo kiểm tra dữ liệu và kiểm thử tham chiếu | Cao | Thêm/sửa/xóa hoạt động; dữ liệu hợp lệ; thao tác nguy cơ mất dữ liệu có xác nhận phù hợp. |
| PB-08 | Trang chi tiết và xem trước định dạng | A; B cung cấp dữ liệu tệp | Hỗ trợ bộ chọn renderer và trạng thái không hỗ trợ | Cao | Trang chi tiết nhận ID, hiển thị đúng thông tin và báo rõ khi không thể xem trước. |
| PB-09 | Ghi chú độc lập, nhiều ghi chú trên một tài liệu, highlight | B nghiệp vụ; A giao diện | Đề xuất ca kiểm thử quan hệ và thao tác CRUD | Cao | Tạo/sửa/xóa từng ghi chú; ghi chú liên kết đúng tài liệu và không lẫn nội dung gốc. |
| PB-10 | Yêu thích, trạng thái đọc, tiến độ và tùy chọn giao diện | B dữ liệu; A giao diện | Kiểm tra trạng thái và persistence sau tải lại | Trung bình | Trạng thái hiển thị nhất quán và được lưu sau khi tải lại. |
| PB-11 | Đăng ký, đăng nhập, Auth Guard, OTP giả lập, đăng xuất | A giao diện; B tích hợp Apps Script/Sheets | Hỗ trợ kiểm tra validation và các nhánh lỗi | Trung bình/cao | Luồng demo hoạt động nếu endpoint sẵn có; OTP được thể hiện rõ là giả lập; lỗi tài khoản được báo; không tuyên bố rằng đăng nhập phân vùng hoặc bảo vệ nội dung IndexedDB. |
| PB-12 | Tóm tắt AI qua gateway và lưu thành ghi chú theo yêu cầu | B gateway; A giao diện | Hỗ trợ định dạng prompt và kiểm thử phản hồi | Trung bình; phụ thuộc dịch vụ | Yêu cầu qua gateway; không lộ khóa trong frontend; chỉ lưu ghi chú khi người dùng chọn và lưu thành công. |
| PB-13 | Knowledge Graph bằng vis-network, gợi ý AI và quyết định người dùng | A hiển thị; B dữ liệu/dịch vụ | Hỗ trợ tạo gợi ý chủ đề và rà soát định dạng phản hồi | Trung bình; phụ thuộc dịch vụ | Node/quan hệ đúng; gợi ý tách khỏi liên kết chính thức; chỉ chấp nhận mới tạo liên kết. |
| PB-14 | Tích hợp, kiểm thử hồi quy và chuẩn bị demo | A + B | Rà soát checklist, đề xuất ca kiểm thử | Cao | Các luồng MVP được kiểm tra; giới hạn và lỗi còn lại được công bố. |

## 6. Kế hoạch commit và bàn giao Git

Nhóm làm trên hai máy theo chuỗi bàn giao tuyến tính, với **đúng 3 commit** và một lần push sau mỗi commit:

| Commit | Thời điểm | Người commit chính | Nội dung |
|---|---|---|---|
| **Commit 1 / Push 1** | Cuối Ngày 2 | A | Nhánh `work/pkb-01-foundation`; tài liệu phạm vi đã review, app shell, điều hướng và Dashboard khung. Message: `feat: add app foundation and dashboard`. |
| **Commit 2 / Push 2** | Cuối Ngày 5 | B | Nhánh `work/pkb-02-data` tạo từ nhánh commit 1; IndexedDB, CRUD và dịch vụ dữ liệu/tích hợp đã sẵn sàng. Message: `feat: add data services and persistence`. |
| **Commit 3 / Push 3** | Cuối Ngày 7 | A | Nhánh `work/pkb-03-integration` tạo từ nhánh commit 2; UI Kho/chi tiết, tích hợp, hồi quy và tài liệu demo. Message: `feat: complete MVP integration and demo readiness`. |

Quy trình mỗi lần bàn giao:

1. Người nhận kiểm tra `git status`, lưu/stash an toàn thay đổi riêng nếu có, rồi `git fetch origin`.
2. Tạo nhánh giai đoạn mới từ nhánh remote vừa bàn giao; không tạo nhánh từ nhánh chính cũ.
3. Trước commit, review `git diff`, chạy kiểm tra phù hợp và chỉ stage tệp thuộc phạm vi chặng.
4. Tạo đúng commit của chặng, push nhánh mới và gửi SHA, tên nhánh, nội dung/tệp đã push cho người kế tiếp.
5. Người nhận checkout nhánh remote đó, xác minh SHA và chạy smoke test trước khi sửa tiếp.

Các chặng không làm song song trên cùng tệp hoặc tạo nhánh độc lập cùng một base. Không tạo merge commit; nhánh cuối chứa chuỗi cả ba commit và là nhánh bàn giao hoàn chỉnh. Nếu cần cập nhật nhánh chính, chỉ dùng fast-forward theo chính sách repo, không tạo commit thứ tư hoặc push lần thứ tư. Không commit khóa API, token, mật khẩu hoặc dữ liệu cá nhân thật.

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
- Có đúng 3 commit theo ba mốc bàn giao; người nhận đã fetch/pull đúng SHA trước khi làm tiếp.
- Demo và tài liệu nêu rõ chức năng hoàn thành, chưa hoàn thành và dịch vụ ngoài còn phụ thuộc.