# Prompt theo tác vụ — 7 ngày, 4 Pull Request

Lịch làm tuần tự trên hai máy. Mỗi PR có prompt riêng cho từng tác vụ; các lệnh Git được tách thành checklist riêng, không gộp vào prompt giao việc.

| PR | Ngày | Người thực hiện | Người review | Mục tiêu |
|---|---|---|---|---|
| PR 1 | 1–2 | Tống Ngọc Minh Châu (M.Châu) | Phan Thị Ngọc Duyên (N.Duyên), nhóm trưởng | Chốt phạm vi, app shell, điều hướng và Dashboard khung |
| PR 2 | 3–4 | Phan Thị Ngọc Duyên (N.Duyên), nhóm trưởng | M.Châu | IndexedDB, CRUD và dịch vụ dữ liệu |
| PR 3 | 5–6 | M.Châu | N.Duyên | Tích hợp UI Kho/chi tiết/ghi chú/tài khoản/Knowledge Graph |
| PR 4 | 7 và thời gian chốt | N.Duyên, nhóm trưởng | M.Châu | Rà soát toàn bộ ứng dụng, sửa lỗi và hoàn tất chức năng trong backlog |

## Quy tắc dùng prompt

1. Đầu mỗi phiên, dán **Prompt nền**, sau đó dán đúng prompt tác vụ.
2. Mỗi prompt chỉ giải quyết một tác vụ nhỏ. Xác nhận kết quả rồi mới chuyển prompt tiếp theo.
3. PR tiếp theo chỉ bắt đầu sau khi PR trước được review và squash-merge vào nhánh chính.
4. Nếu reviewer yêu cầu sửa, cập nhật trên đúng nhánh và PR đang mở; không tạo PR thay thế.
5. Tạo đúng 4 PR. Mỗi PR dùng **Squash and merge**, tương ứng một commit tích hợp trên nhánh chính.

## Prompt nền — dùng đầu mỗi phiên

```text
Bạn đang hỗ trợ dự án Personal Knowledge Base. Trước khi làm tác vụ, đọc .ai/AGENTS.md, .ai/SKILLS.md và phần liên quan trong architecture.md, data-contract.md, user-stories.md, product-backlog.md.

Kiểm tra mã nguồn và trạng thái Git thực tế trước khi sửa. Không coi tính năng trong tài liệu là đã triển khai. Giữ nguyên thay đổi có sẵn. Chỉ thực hiện đúng tác vụ được giao; không tự làm các mục khác trong PR.

Tuân thủ quyết định hiện tại: HTML/CSS/JavaScript thuần; nội dung/tệp dùng IndexedDB; tùy chọn nhỏ và phiên đăng nhập demo dùng localStorage. Đăng nhập/OTP là demo, dữ liệu IndexedDB không phân vùng theo tài khoản. API AI chỉ đi qua gateway phía máy chủ; không đưa khóa bí mật vào frontend. Gợi ý AI chỉ thành liên kết chính thức khi người dùng chấp thuận.

Nếu yêu cầu xung đột với tài liệu hoặc mã, nêu chính xác điểm xung đột và hỏi trước khi thay đổi phạm vi, kiến trúc, bảo mật hoặc hợp đồng dữ liệu. Sau tác vụ, báo tệp đã đổi, kiểm tra đã chạy và việc còn bị chặn. Không tự tạo/merge PR.
```

## PR 1 — Phạm vi, app shell và Dashboard

**Lịch:** Ngày 1–2. **Tác giả:** M.Châu. **Reviewer:** N.Duyên (nhóm trưởng).

### Prompt 1.1 — Chốt màn hình và luồng

```text
Đối chiếu user-stories.md với architecture.md. Lập danh sách màn hình MVP, luồng điều hướng và tiêu chí nghiệm thu cho PR 1. Đánh dấu điểm chưa chốt và phụ thuộc dịch vụ/dữ liệu cần N.Duyên xác nhận. Không tự thay đổi phạm vi hoặc schema. Bàn giao danh sách cho N.Duyên review trước khi triển khai UI.
```

### Prompt 1.2 — Dựng app shell và điều hướng

```text
Triển khai app shell theo architecture.md: khung trang, khu vực điều hướng, vùng nội dung và đường vào các màn hình MVP. Dùng HTML/CSS/JavaScript thuần theo cấu trúc mã đang có. Không thêm framework, thư viện, build step hoặc lưu trữ mới. Mục chưa triển khai phải được thể hiện là placeholder, không giả vờ chức năng đã tồn tại.
```

### Prompt 1.3 — Làm layout responsive

```text
Hoàn thiện responsive cho app shell trên desktop và mobile. Bảo đảm điều hướng dùng được bằng bàn phím, có focus state nhìn thấy được, không tràn ngang và không che khuất nội dung. Chỉ sửa CSS liên quan trực tiếp đến khung ứng dụng.
```

### Prompt 1.4 — Dựng Dashboard

```text
Tạo giao diện Dashboard gồm tài liệu mới thêm, vừa mới xem, thống kê và truy cập nhanh theo architecture.md. Nếu chưa có service dữ liệu, dùng trạng thái rỗng hoặc dữ liệu mẫu được nhận diện rõ là mẫu; không truy cập IndexedDB trực tiếp và không tuyên bố dữ liệu thật đã được kết nối. Thống kê tách số tài liệu và ghi chú.
```

### Prompt 1.5 — Review phạm vi PR 1

```text
Rà soát riêng app shell, điều hướng, responsive và Dashboard của PR 1. Xác minh link/đường điều hướng, trạng thái rỗng, lỗi console nếu có công cụ và diff không chứa phần ngoài phạm vi. Báo kết quả và giới hạn; không thực hiện thao tác Git.
```

### Thao tác Git và PR 1

**M.Châu tạo nhánh mới từ nhánh chính cập nhật:**

```powershell
git status
git fetch origin
git switch <main-branch>
git pull --ff-only origin <main-branch>
git switch -c feature/pkb-pr1-foundation
```

Sau khi N.Duyên review tác vụ:

```powershell
git diff
git diff --check
git add <các-tệp-thuộc-PR1>
git diff --cached
git commit -m "feat: add app foundation and dashboard"
git push -u origin feature/pkb-pr1-foundation
```

Tạo PR vào `<main-branch>`:

- Title: `PR 1: App foundation and dashboard`
- Reviewer: N.Duyên.
- Mô tả: phạm vi, các tác vụ hoàn thành, kiểm tra và giới hạn.
- N.Duyên review; sau khi đạt, chọn **Squash and merge**. M.Châu cập nhật nhánh chính sau merge trước khi làm PR 3.

## PR 2 — IndexedDB và dịch vụ dữ liệu

**Lịch:** Ngày 3–4. **Tác giả:** N.Duyên (nhóm trưởng). **Reviewer:** M.Châu.

### Prompt 2.1 — Thiết kế IndexedDB

```text
Đọc data-contract.md, xác định object stores, key/index cần thiết và cách khởi tạo/versioning IndexedDB. Đối chiếu schema với các entity/quan hệ hiện có. Không tự đổi tên trường hoặc quy tắc nghiệp vụ. Trình bày ngắn thiết kế và các rủi ro migration để M.Châu review trước khi triển khai.
```

### Prompt 2.2 — Khởi tạo database và lớp truy cập

```text
Triển khai mở/khởi tạo IndexedDB và lớp truy cập dùng chung theo thiết kế đã review. Xử lý lỗi open/upgrade/transaction rõ ràng; không báo sẵn sàng nếu khởi tạo thất bại. Không để component giao diện tự thao tác IndexedDB.
```

### Prompt 2.3 — CRUD tài liệu và URL

```text
Triển khai DocumentService theo data-contract.md: create, get by ID, list, update, soft delete, restore và permanent delete nếu nằm trong phạm vi. Validate title, type, sourceUrl, storageKey, folderId/tagIds và tham chiếu. Chỉ trả thành công sau khi transaction hoàn tất; trả lỗi rõ ràng khi dữ liệu sai hoặc lưu thất bại.
```

### Prompt 2.4 — FolderService và TagService

```text
Triển khai dịch vụ thư mục và tag theo hợp đồng dữ liệu. Kiểm tra tên rỗng/trùng, vòng lặp thư mục và tham chiếu entity. Không xóa thư mục còn tài liệu/thư mục con hoặc tag còn được dùng; trả thông báo hướng dẫn xử lý thay vì xóa âm thầm.
```

### Prompt 2.5 — Note, Highlight và trạng thái đọc

```text
Triển khai dịch vụ Note, Highlight, ReadingProgress, yêu thích và trạng thái đọc theo data-contract.md. Hỗ trợ ghi chú độc lập và nhiều ghi chú trên cùng tài liệu; không trộn nội dung ghi chú với file gốc. Khi cập nhật/xóa entity, duy trì tham chiếu đúng theo quy tắc.
```

### Prompt 2.6 — Lọc dữ liệu và tích hợp ngoài nếu sẵn sàng

```text
Triển khai helper/service lọc và sắp xếp có thể kết hợp tìm kiếm với bộ lọc. Tùy chọn nhỏ lưu ở localStorage, gồm Card/List và số mục 10/20/50/all, mặc định 10. Chỉ tích hợp Google Apps Script hoặc AI gateway nếu endpoint và hợp đồng request/response được cung cấp; nếu thiếu, ghi rõ bị chặn. Không đưa khóa bí mật vào frontend, không giả lập thành công.
```

### Prompt 2.7 — Kiểm thử hợp đồng dịch vụ

```text
Kiểm thử IndexedDB/service: CRUD, dữ liệu sai, tham chiếu không tồn tại, lỗi transaction/storage, đọc lại sau reload và quy tắc xóa/khôi phục. Viết hoặc cập nhật mô tả API service gồm tên hàm, input, output và lỗi để M.Châu tích hợp. Báo ca kiểm thử đã chạy và kết quả; không thực hiện thao tác Git.
```

### Thao tác Git và PR 2

Chỉ sau khi PR 1 đã squash-merge. **N.Duyên tạo nhánh mới:**

```powershell
git status
git fetch origin
git switch <main-branch>
git pull --ff-only origin <main-branch>
git switch -c feature/pkb-pr2-data
```

Sau khi M.Châu review dịch vụ:

```powershell
git diff
git diff --check
git add <các-tệp-IndexedDB-và-service-thuộc-PR2>
git diff --cached
git commit -m "feat: add data services and persistence"
git push -u origin feature/pkb-pr2-data
```

Tạo PR:

- Title: `PR 2: IndexedDB and data services`
- Reviewer: M.Châu.
- Mô tả: schema/store, API service, kiểm thử, rủi ro migration và tích hợp ngoài bị chặn.
- M.Châu review; sau khi đạt, chọn **Squash and merge**. N.Duyên và M.Châu cập nhật nhánh chính trước PR 3.

## PR 3 — Tích hợp giao diện và luồng MVP

**Lịch:** Ngày 5–6. **Tác giả:** M.Châu. **Reviewer:** N.Duyên (nhóm trưởng).

### Prompt 3.1 — Tích hợp Dashboard với dữ liệu thật

```text
Kết nối Dashboard với các service đã merge trong PR 2: tài liệu mới thêm, vừa mới xem, thống kê riêng tài liệu/ghi chú và truy cập nhanh. Không gọi IndexedDB trực tiếp từ UI. Tài liệu trong trash không được tính vào kho hoạt động. Hiển thị loading, empty và lỗi.
```

### Prompt 3.2 — Kho tài liệu

```text
Triển khai UI Kho dạng Card/List, tìm kiếm/gợi ý, lọc theo tiêu chí được hỗ trợ, sắp xếp và phân trang 10/20/50/all. Tích hợp qua service. Tìm kiếm, lọc và sắp xếp phải kết hợp chính xác, không tải lại trang. Bổ sung trạng thái loading, không kết quả và lỗi.
```

### Prompt 3.3 — Trang chi tiết và renderer

```text
Tạo trang chi tiết nhận ID, đọc dữ liệu qua service và hiển thị metadata/tag/trạng thái. Chọn renderer theo định dạng thực sự được hỗ trợ trong data-contract.md. Khi không xem trước được, thông báo rõ và cho tải xuống nếu phù hợp; lỗi preview không được làm hỏng file gốc.
```

### Prompt 3.4 — UI ghi chú và trạng thái

```text
Tích hợp UI tạo/sửa/xóa ghi chú độc lập và ghi chú gắn với tài liệu, highlight, yêu thích, trạng thái đọc và tiến độ qua service của PR 2. Giữ ghi chú tách biệt khỏi nội dung file. Chỉ hiện thành công sau khi service xác nhận lưu; giữ input để thử lại khi lưu thất bại nếu có thể.
```

### Prompt 3.5 — Tài khoản demo và Knowledge Graph

```text
Tích hợp giao diện tài khoản theo endpoint có thật và Knowledge Graph bằng vis-network. Ghi rõ OTP là demo, dữ liệu IndexedDB không phân vùng theo tài khoản và Auth Guard client-side không phải bảo mật. Gợi ý AI phải tách khỏi link đã xác nhận; chỉ chấp nhận mới tạo link. Endpoint/gateway thiếu thì hiển thị giới hạn, không giả lập thành công.
```

### Prompt 3.6 — Responsive, điều hướng và review PR 3

```text
Kiểm tra UI Kho, chi tiết, ghi chú, tài khoản và graph trên desktop/mobile; sửa lỗi responsive/điều hướng trong phạm vi PR 3. Chạy smoke test các luồng liên quan, kiểm tra lỗi console và trạng thái loading/rỗng/lỗi. Báo kết quả cho N.Duyên review; không thực hiện thao tác Git.
```

### Thao tác Git và PR 3

Chỉ sau khi PR 2 đã squash-merge. **M.Châu tạo nhánh mới:**

```powershell
git status
git fetch origin
git switch <main-branch>
git pull --ff-only origin <main-branch>
git switch -c feature/pkb-pr3-integration
```

Sau khi N.Duyên review:

```powershell
git diff
git diff --check
git add <các-tệp-UI-và-tích-hợp-thuộc-PR3>
git diff --cached
git commit -m "feat: integrate MVP user workflows"
git push -u origin feature/pkb-pr3-integration
```

Tạo PR:

- Title: `PR 3: Integrate MVP user workflows`
- Reviewer: N.Duyên.
- Mô tả: các tác vụ 3.1–3.6, luồng kiểm tra, ảnh giao diện và phần phụ thuộc còn thiếu.
- Sau khi duyệt, **Squash and merge**. PR 4 chỉ bắt đầu từ nhánh chính đã cập nhật.

## PR 4 — Chốt ứng dụng, sửa lỗi và hoàn tất chức năng

**Lịch:** Ngày 7 và thời gian chốt theo nghiệm thu. **Tác giả/điều phối:** N.Duyên (nhóm trưởng). **Reviewer UI:** M.Châu.

PR này là vòng hoàn thiện cuối: rà soát toàn bộ chức năng đã duyệt, xử lý lỗi phát hiện ở PR 1–3 và hoàn tất các hạng mục backlog còn thiếu trong phạm vi. Không tự mở rộng phạm vi; yêu cầu mới cần Product Owner duyệt.

### Prompt 4.1 — Lập checklist nghiệm thu từ backlog

```text
Đóng vai N.Duyên, nhóm trưởng và tác giả PR 4. Đối chiếu toàn bộ acceptance criteria trong user-stories.md, architecture.md, data-contract.md và backlog với code hiện tại sau khi PR 3 đã merge. Lập checklist theo trạng thái: đạt, lỗi, chưa triển khai, bị chặn bởi endpoint/gateway. Không sửa code ở bước này; gửi M.Châu review checklist và ưu tiên lỗi.
```

### Prompt 4.2 — Sửa lỗi hồi quy ưu tiên cao

```text
Dựa trên checklist đã được review, sửa các lỗi mức nghiêm trọng/cao thuộc phạm vi đã duyệt, ưu tiên lỗi làm hỏng luồng CRUD, mất dữ liệu, sai tham chiếu, điều hướng hoặc trạng thái thành công giả. Mỗi lỗi phải tái hiện được trước khi sửa và có bước xác minh sau sửa. Không thay đổi schema/kiến trúc nếu chưa được thống nhất.
```

### Prompt 4.3 — Hoàn tất chức năng backlog còn thiếu

```text
Kiểm tra các tiêu chí backlog đã duyệt nhưng còn thiếu trong code. Hoàn thiện các phần còn trong phạm vi PR 4, ưu tiên luồng cốt lõi: lưu bền vững, CRUD, tìm kiếm/lọc/phân trang, ghi chú và trạng thái đọc/yêu thích. Với endpoint/gateway chưa có, không giả lập; ghi rõ bị chặn và hoàn thiện trạng thái lỗi/giao diện giới hạn nếu phù hợp. Không thêm tính năng ngoài backlog.
```

### Prompt 4.4 — Kiểm thử hồi quy toàn ứng dụng

```text
Chạy bộ kiểm tra nhỏ nhất bao phủ các luồng MVP và hồi quy toàn ứng dụng: tạo/sửa/xóa/khôi phục dữ liệu, reload, tham chiếu, tìm kiếm/lọc/sắp xếp/phân trang, ghi chú, trạng thái, responsive, lỗi lưu/API và Knowledge Graph nếu gateway sẵn có. Ghi rõ lệnh/ca kiểm tra và kết quả thực tế. Không tuyên bố đã kiểm tra nếu chưa chạy.
```

### Prompt 4.5 — Rà soát bảo mật, tài liệu và demo

```text
Rà soát PR 4 để bảo đảm không có khóa/token/dữ liệu cá nhân trong mã hoặc tài liệu; đăng nhập demo và OTP được mô tả đúng giới hạn; AI đi qua gateway; đề xuất graph cần người dùng duyệt. Cập nhật README, CHANGELOG và kịch bản demo chỉ theo chức năng đã xác minh. Tạo danh sách lỗi/giới hạn còn lại và xin M.Châu review cuối.
```

### Prompt 4.6 — Review chéo và tiêu chí merge

```text
Review toàn bộ diff PR 4 cùng checklist nghiệm thu. Phân loại lỗi còn lại theo mức độ, xác nhận mỗi sửa đổi có kiểm thử phù hợp, không có thay đổi ngoài phạm vi và các giới hạn dịch vụ được công bố. Chỉ đề xuất merge khi không còn lỗi nghiêm trọng/cao chưa xử lý; nếu còn, nêu rõ việc cần hoàn tất trong chính PR 4.
```

### Thao tác Git và PR 4

Chỉ sau khi PR 3 đã squash-merge. **N.Duyên tạo nhánh mới từ nhánh chính mới nhất:**

```powershell
git status
git fetch origin
git switch <main-branch>
git pull --ff-only origin <main-branch>
git switch -c feature/pkb-pr4-finalization
```

Sau khi hoàn tất prompt 4.1–4.6 và M.Châu review:

```powershell
git diff
git diff --check
git add <các-tệp-sửa-lỗi-hoàn-thiện-và-tài-liệu-thuộc-PR4>
git diff --cached
git commit -m "fix: finalize MVP and resolve acceptance issues"
git push -u origin feature/pkb-pr4-finalization
```

Tạo PR cuối:

- Title: `PR 4: Finalize MVP and resolve acceptance issues`
- Reviewer: M.Châu.
- Mô tả: checklist đạt/chưa đạt/bị chặn, lỗi đã sửa, kiểm thử và giới hạn còn lại.
- N.Duyên điều phối review và xác nhận tiêu chí; M.Châu review giao diện/luồng. Sau khi đạt, chọn **Squash and merge**. Không tạo PR thứ năm.

## Checklist Git chung cho người review/nhận PR

1. Xác nhận PR có base là nhánh chính mới nhất và compare đúng feature branch.
2. Đọc mô tả, Files changed, kiểm tra secrets và xác nhận phạm vi đúng PR.
3. Chạy hoặc xác minh tiêu chí nghiệm thu tương ứng.
4. Nếu cần sửa, yêu cầu tác giả cập nhật cùng nhánh/PR.
5. Chỉ squash-merge khi đạt; sau merge, người tiếp theo fetch/pull nhánh chính trước khi tạo branch mới.

Lịch tổng: **PR 1 M.Châu (Ngày 1–2) → PR 2 N.Duyên (Ngày 3–4) → PR 3 M.Châu (Ngày 5–6) → PR 4 N.Duyên, nhóm trưởng (Ngày 7/chốt ứng dụng).** Nhánh chính nhận đúng bốn commit tích hợp từ bốn lần squash-merge.
