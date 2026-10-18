# Prompt làm việc trên hai máy — 7 ngày, đúng 3 commit

Lịch bàn giao tuần tự giữa hai máy:

1. **Chặng 1, Ngày 1–2: A làm → A commit/push → B lấy về.**
2. **Chặng 2, Ngày 3–5: B làm trên nhánh mới → B commit/push → A lấy về.**
3. **Chặng 3, Ngày 5–7: A làm trên nhánh mới → A commit/push → B nghiệm thu.**

Mỗi chặng chỉ có một commit và một lần push. Không phát triển đồng thời trên hai nhánh độc lập, không tạo commit phụ để chuyển code.

## Quy ước Git

- Thay `<main-branch>` bằng tên nhánh chính thực tế của repository, ví dụ `main` hoặc `master`.
- Các nhánh bàn giao nối tiếp nhau:
  - `work/pkb-01-foundation`
  - `work/pkb-02-data`, bắt đầu từ nhánh chặng 1
  - `work/pkb-03-integration`, bắt đầu từ nhánh chặng 2
- Prompt làm việc bên dưới chỉ yêu cầu AI thực hiện phần kỹ thuật. **Các lệnh Git nằm ở mục riêng**, không cần dán lệnh Git vào prompt công việc.
- Người nhận chỉ bắt đầu làm sau khi đã fetch nhánh, xác minh SHA và xác nhận với người gửi.
- Các lệnh `git add -A` bên dưới chỉ an toàn khi working tree sạch lúc bắt đầu chặng và mọi thay đổi hiện tại đều do người phụ trách chặng tạo. Nếu `git status` cho thấy thay đổi khác, không chạy `git add -A`; dừng và xác định phạm vi trước.
- Nhánh chặng 3 chứa đủ ba commit và là nhánh bàn giao cuối. Không tạo merge commit hoặc push lần thứ tư để cập nhật nhánh chính. Nếu cần tích hợp nhánh chính, dùng PR/fast-forward theo chính sách repository mà không tạo commit mới.
- Không force-push. Nếu working tree không sạch, dừng và xử lý thay đổi hiện có an toàn trước khi chạy lệnh chuyển nhánh.

## Prompt nền — dán trước prompt công việc mỗi phiên

```text
Bạn đang hỗ trợ dự án Personal Knowledge Base. Trước khi làm việc, đọc .ai/AGENTS.md, .ai/SKILLS.md và các phần liên quan trong architecture.md, data-contract.md, user-stories.md, product-backlog.md.

Kiểm tra cấu trúc mã nguồn thực tế; không giả định tính năng đã tồn tại chỉ vì tài liệu mô tả. Giữ nguyên thay đổi có sẵn. Chỉ thực hiện phạm vi và vai trò được giao trong prompt công việc tiếp theo.

Tuân thủ quyết định dự án: HTML/CSS/JavaScript thuần; nội dung và tệp dùng IndexedDB; tùy chọn nhỏ và phiên demo dùng localStorage. Đăng nhập/OTP là demo, dữ liệu IndexedDB không phân vùng theo tài khoản. API AI chỉ gọi qua gateway phía máy chủ, không để lộ khóa. Gợi ý AI chỉ trở thành liên kết chính thức khi người dùng chấp thuận.

Nếu tài liệu, mã nguồn hoặc yêu cầu mâu thuẫn, nêu rõ và hỏi trước khi thay đổi kiến trúc, bảo mật hoặc hợp đồng dữ liệu. Sau khi làm, báo tệp đã sửa, kiểm tra đã chạy và phần còn bị chặn. Không tự chạy lệnh commit/push; các thao tác Git do nhóm thực hiện riêng theo checklist của chặng.
```

## Chặng 1 — Ngày 1–2: A dựng nền, bàn giao cho B

**Phân công:** A thực hiện; B review phạm vi và hợp đồng dữ liệu.

**Phạm vi:** PB-01, PB-03, PB-05 ở mức khung.

### Prompt công việc cho A

```text
Thực hiện Chặng 1 (Ngày 1–2) với vai trò Thành viên A.

Đọc user-stories.md và architecture.md; phối hợp Thành viên B để thống nhất phạm vi MVP, màn hình, luồng điều hướng và tiêu chí nghiệm thu. Nhờ B review data-contract.md; không tự đổi schema.

Xây dựng app shell, điều hướng, layout responsive và Dashboard khung theo backlog. Có thể dùng trạng thái rỗng hoặc dữ liệu mẫu. Không truy cập IndexedDB trực tiếp, không giả lập dịch vụ dữ liệu đã có và không làm các tính năng thuộc chặng sau.

Kiểm tra kết quả phù hợp với mã hiện có. Bàn giao danh sách màn hình/luồng và các điểm cần B review.
```

### Thao tác Git của A — tạo và push commit 1

Chạy lần lượt trong terminal tại thư mục repository. Nếu `git status` cho thấy thay đổi không thuộc chặng này hoặc thay đổi chưa rõ nguồn gốc, dừng để kiểm tra trước.

```powershell
git status
git fetch origin
git switch <main-branch>
git pull --ff-only origin <main-branch>
git switch -c work/pkb-01-foundation
```

Sau khi hoàn thành công việc và B đã review:

```powershell
git status
git diff
git diff --check
git add -A
git diff --cached
git commit -m "feat: add app foundation and dashboard"
git push -u origin work/pkb-01-foundation
git rev-parse HEAD
```

A gửi B tên nhánh, SHA từ `git rev-parse HEAD`, nội dung/tệp đã bàn giao và kết quả kiểm tra. Đây là **commit 1 / push 1**.

### Thao tác Git của B — nhận commit 1, tạo nhánh chặng 2

B chỉ chạy sau khi working tree sạch hoặc các thay đổi cục bộ đã được xử lý an toàn:

```powershell
git status
git fetch origin
git switch -c work/pkb-02-data origin/work/pkb-01-foundation
git rev-parse HEAD
git log -1 --oneline
```

B đối chiếu SHA với thông tin A gửi, kiểm tra cấu trúc/ứng dụng rồi xác nhận đã nhận đúng nhánh. **Chưa commit hoặc push** ở bước nhận bàn giao.

## Chặng 2 — Ngày 3–5: B làm dữ liệu/dịch vụ, bàn giao cho A

**Phân công:** B thực hiện; A review hợp đồng dịch vụ và kiểm tra diff.

**Phạm vi:** PB-02, PB-04, PB-07, PB-09, PB-10; dịch vụ PB-11/PB-12/PB-13 nếu endpoint/gateway sẵn sàng.

### Prompt công việc cho B

```text
Thực hiện Chặng 2 (Ngày 3–5) với vai trò Thành viên B trên nhánh work/pkb-02-data đã được tạo từ commit bàn giao của A.

Triển khai IndexedDB và dịch vụ theo data-contract.md: CRUD tài liệu/URL/tag/thư mục; ghi chú độc lập và ghi chú liên kết tài liệu; highlight; tiến độ đọc; yêu thích; các thao tác dữ liệu cần thiết cho UI. UI không được truy cập IndexedDB trực tiếp.

Kiểm tra validation, tham chiếu entity, lỗi transaction, quy tắc xóa/khôi phục và khả năng đọc lại sau tải trang. Chuẩn bị hợp đồng dịch vụ dễ tích hợp, gồm tên hàm, tham số, kết quả, lỗi và ví dụ dữ liệu; gửi A review trước khi chốt.

Chỉ tích hợp Google Apps Script/Sheets hoặc AI gateway nếu endpoint và hợp đồng đã được cung cấp. Nếu thiếu, ghi rõ phần bị chặn; không giả lập thành công và không đưa khóa vào frontend. Báo kết quả, kiểm tra đã chạy và giới hạn còn lại.
```

### Thao tác Git của B — kiểm tra, commit và push commit 2

Trước khi sửa, B xác nhận đang ở nhánh mới từ commit 1:

```powershell
git status
git branch --show-current
git log -1 --oneline
```

Sau khi hoàn tất và A đã review:

```powershell
git status
git diff
git diff --check
git add -A
git diff --cached
git commit -m "feat: add data services and persistence"
git push -u origin work/pkb-02-data
git rev-parse HEAD
```

B gửi A tên nhánh, SHA, nội dung/tệp và kết quả kiểm tra. Đây là **commit 2 / push 2**.

### Thao tác Git của A — nhận commit 2, tạo nhánh chặng 3

A chỉ chạy sau khi B thông báo push thành công:

```powershell
git status
git fetch origin
git switch -c work/pkb-03-integration origin/work/pkb-02-data
git rev-parse HEAD
git log --oneline -3
```

A xác nhận SHA cuối đúng với SHA B gửi và lịch sử có commit chặng 1, chặng 2; chạy smoke test dịch vụ và xác nhận đã nhận trước khi tích hợp UI.

## Chặng 3 — Ngày 5–7: A tích hợp, bàn giao cho B nghiệm thu

**Phân công:** A thực hiện; B review và nghiệm thu trên máy riêng.

**Phạm vi:** PB-06, PB-08, phần UI PB-09–PB-13 và PB-14.

### Prompt công việc cho A

```text
Thực hiện Chặng 3 (Ngày 5–7) trên nhánh work/pkb-03-integration đã tạo từ commit của B.

Tích hợp Dashboard với dịch vụ. Hoàn thiện UI Kho: Card/List, tìm kiếm/gợi ý, lọc, sắp xếp và phân trang 10/20/50/tất cả. Hoàn thiện chi tiết tài liệu, renderer theo định dạng được hỗ trợ, ghi chú/highlight/trạng thái đọc, tùy chọn giao diện, responsive và điều hướng.

Tích hợp giao diện tài khoản demo và Knowledge Graph bằng vis-network. Nêu rõ OTP là demo, IndexedDB không phân vùng theo tài khoản và Auth Guard không phải bảo mật. Gợi ý AI không thành liên kết chính thức nếu người dùng chưa chấp thuận.

Hiển thị trạng thái loading/rỗng/lỗi/thành công chính xác; không báo thành công khi lưu/API thất bại. Cập nhật README/tài liệu demo theo chức năng đã kiểm chứng, ghi rõ endpoint/gateway hoặc tính năng nào còn bị chặn.

Kiểm tra các luồng chính và nhờ B review diff/kết quả. Báo tệp đã sửa, kiểm tra đã chạy, lỗi còn lại và giới hạn.
```

### Thao tác Git của A — review, commit và push commit 3

Chỉ tiếp tục sau khi B đã review và working tree không có thay đổi ngoài phạm vi:

```powershell
git status
git branch --show-current
git diff
git diff --check
```

Stage có chọn lọc, review staged diff rồi tạo commit cuối:

```powershell
git add -A
git diff --cached
git commit -m "feat: complete MVP integration and demo readiness"
git push -u origin work/pkb-03-integration
git rev-parse HEAD
git log --oneline -3
```

A gửi B SHA, nhánh, danh sách nội dung/tệp và kết quả kiểm tra. Đây là **commit 3 / push 3 và lần push cuối cùng**. Không push nhánh chính riêng.

### Thao tác Git của B — nhận bản cuối và nghiệm thu

```powershell
git status
git fetch origin
git switch -c verify/pkb-final origin/work/pkb-03-integration
git rev-parse HEAD
git log --oneline -3
```

B đối chiếu SHA, xác nhận có đúng ba commit của ba chặng và chạy smoke/regression test. Nhánh `verify/pkb-final` chỉ dùng để kiểm tra cục bộ, **không commit/push**. Báo A kết quả nghiệm thu; không tạo commit thứ tư.

## Tóm tắt đúng 3 mốc bàn giao

| Mốc | Người làm/push | Nhánh được push | Người nhận và thao tác |
|---|---|---|---|
| Cuối Ngày 2 | A — commit 1, push 1 | `work/pkb-01-foundation` | B fetch, tạo `work/pkb-02-data` từ nhánh này |
| Cuối Ngày 5 | B — commit 2, push 2 | `work/pkb-02-data` | A fetch, tạo `work/pkb-03-integration` từ nhánh này |
| Cuối Ngày 7 | A — commit 3, push 3 | `work/pkb-03-integration` | B fetch nhánh kiểm tra cục bộ và nghiệm thu |

Không tạo commit/push ngoài ba mốc. Nếu chặng bị trễ, lùi thời điểm bàn giao thay vì tạo commit phụ. Không force-push, không tạo merge commit và không cập nhật nhánh chính bằng push thứ tư.
