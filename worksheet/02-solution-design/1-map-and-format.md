---
artifact: 1 — FINAL kế hoạch giải pháp
bai-tap: 2 — Thiết kế giải pháp
phase: Chọn rủi ro + chọn tầng + chọn demo + chốt 3 lớp giải pháp
time: 11:00-11:55
input: 00-context.md + 01-test-set-review/3-FINAL-test-set-eval-plan.md
nop-cuoi: Có — file cuối Bài 2
---

# 1 — FINAL: Kế hoạch giải pháp

File này ghi lại quyết định chính của Bài 2:

- Rủi ro nào được chọn.
- Vì sao rủi ro đó quan trọng.
- Nguyên nhân gốc là gì.
- Nhóm sẽ xây 3 lớp giải pháp nào.
- Mỗi lớp dùng demo gì.

Lý do cần 3 lớp: một giải pháp đơn lẻ dễ lọt lỗi. Với rủi ro nặng, nhóm cần nhiều lớp cùng đỡ: lớp này ngăn, lớp kia phát hiện, lớp khác khắc phục hoặc thông báo cho người dùng.

Ba lớp giải pháp nằm trong thư mục `artifact/`:

| Lớp | Thư mục | Vai trò |
|---|---|---|
| Giao diện | `artifact/1-uiux/` | Cảnh báo, dẫn nguồn, nút chuyển sang người thật |
| Chỉ dẫn AI | `artifact/2-prompt/` | Hỏi lại, từ chối, bắt buộc dẫn nguồn |
| Kiến trúc dữ liệu | `artifact/3-architecture/` | Tra cứu nguồn đúng, lưu tạm dữ liệu, xử lý khi thiếu nguồn, giám sát |

Ba lớp này bổ sung cho nhau. Nếu một lớp lọt lỗi, lớp khác vẫn có thể chặn hoặc giảm hại.

## Thông tin nhóm

- **Chủ đề**: Track 1 — Chatbot tư vấn tuyển sinh đại học VinUni
- **Thành viên**: Nguyễn Đông Hưng — 2A202600392; Quách Ngọc Quang — 2A202600285
- **Ngày**: 2026-05-13

---

## Phần A — Chọn rủi ro và tầng giải pháp

### Rủi ro chính được chọn

- **ID tình huống**: T-04 (Vượt thẩm quyền eligibility)
- **Mô tả ngắn**: Khi phụ huynh/học sinh hỏi về khả năng đủ điều kiện học bổng (ví dụ: "Con thi 24 điểm, học ở Hà Nội, có đủ điều kiện nhận học bổng Merit 100% không?"), AI có xu hướng tự đánh giá eligibility thay vì chuyển counselor, gây ra quyết định tài chính sai và học sinh có thể bỏ lỡ cơ hội apply trường khác.
- **Mức độ**: Nặng
- **Điểm rủi ro**: 20
- **Vì sao chọn tình huống này**:
  - Là **primary failure** từ Day 24 của Quang
  - Severity cao: học sinh có thể nộp muộn hoặc bỏ trường khác dựa trên dự đoán sai
  - Testability: Có nhiều test cases rõ ràng (T-03, T-04, T-20, T-21)
  - Legal liability: Vi phạm Vietnam AI Law yêu cầu escalation, có thể dẫn đến phạt và kiện (theo Air Canada case)

### Tìm nguyên nhân gốc

Đừng chỉ mô tả lỗi. Hãy trả lời: vì sao lỗi xảy ra?

- [x] **AI được train để "helpful" và "answer questions"**: Model có xu hướng trả lời mọi câu hỏi để thỏa mãn user, thay vì từ chối khi vượt phạm vi.
- [x] **Thiếu explicit escalation rule trong system prompt**: Không có quy tắc rõ ràng "Nếu user hỏi về eligibility → bắt buộc chuyển counselor".
- [x] **Giao diện không cảnh báo limitation**: Không có disclaimer nào cho user biết chatbot không thể đánh giá eligibility.
- [x] **Không có eligibility classifier**: Hệ thống không phân biệt được câu hỏi thông thường (ví dụ: "Deadline học bổng là gì?") với câu hỏi cần escalate (ví dụ: "Con thi 24 điểm có đủ điều kiện không?").
- [ ] Thiếu audit log để theo dõi trường hợp từ chối → khó monitor lỗi sau khi ra mắt.

### Bảng nối nguyên nhân với tầng sửa

| Nguyên nhân gốc | Tầng ưu tiên sửa | Lớp giải pháp liên quan |
|---|---|---|
| Thiếu explicit escalation rule: Model được train "helpful" nên tự trả lời eligibility thay vì từ chối | Prompt / Human Process | `2-prompt` là chính (thêm rule), `3-architecture` hỗ trợ (classifier) |
| UI thiếu cảnh báo về limitation: User tin chatbot có thẩm quyền đánh giá eligibility | Giao diện (UI/UX) | `1-uiux` là chính (disclaimer + escalation button) |
| Không có eligibility classifier: Hệ thống không phân biệt được câu hỏi thông thường vs câu hỏi cần escalate | Kiến trúc (Architecture) | `3-architecture` là chính (thêm module classifier trước RAG) |
| Knowledge base không cover đủ eligibility scenarios: Model phải đoán khi không có dữ liệu | Dữ liệu / RAG | `3-architecture` hỗ trợ (fallback mechanism) |

Nguyên tắc: lỗi ở tầng nào, ưu tiên sửa ở tầng đó. Đừng chỉ thêm cảnh báo giao diện nếu nguyên nhân gốc là thiếu nguồn dữ liệu hoặc AI đoán khi không biết.

### 10 tầng giải pháp tham khảo

Không bắt buộc dùng đủ 10 tầng. Bảng này giúp nhóm chọn đúng hướng sửa.

| Tầng | Khi nào dùng |
|---|---|
| Giao diện | Người dùng tin AI quá mức, thiếu cảnh báo, thiếu nguồn, thiếu nút chuyển sang người thật |
| Chỉ dẫn AI | AI đoán khi không biết, không hỏi lại, không từ chối |
| Quy trình xử lý | Cần phân loại ý định, chuyển đúng nơi xử lý, có cách xử lý khi AI không nên trả lời |
| Dữ liệu / tra cứu nguồn (RAG) | Thiếu nguồn đúng, nguồn cũ, AI không dựa vào nguồn đáng tin cậy |
| Theo dõi | Lỗi lặp lại sau khi ra mắt nhưng không ai thấy |
| Chính sách / thông báo giới hạn | Người dùng không biết giới hạn của AI |
| Người duyệt / phê duyệt | Tình huống pháp lý, y tế, tài chính, tuyển dụng, hoặc tác động lớn |
| Vai trò trách nhiệm | Có cảnh báo nhưng không ai chịu trách nhiệm xử lý |
| Vòng phản hồi | Cần người dùng / người rà báo lỗi để cập nhật hệ thống |
| Kiến trúc lai | LLM một mình không đủ, cần rule, classifier, hoặc nhiều bước kiểm tra |

### 4 hành động phòng vệ

Mỗi lớp nên làm ít nhất một việc:

- **Ngăn**: giảm khả năng lỗi xảy ra từ đầu.
- **Phát hiện**: nhận ra lỗi hoặc tín hiệu nguy hiểm.
- **Khắc phục**: chuyển sang người thật, dùng câu trả lời dự phòng, hoặc dừng trả lời.
- **Thông báo**: giúp người dùng hiểu mức tin cậy và rủi ro.

Gợi ý theo mức rủi ro:

| Mức rủi ro | Nên có |
|---|---|
| Nhẹ | Ít nhất 1 hành động |
| Vừa | Ít nhất 2 hành động |
| Nặng | Ít nhất 3 hành động |
| Rất nặng / không đảo ngược được | Cố gắng đủ 4 hành động + có người chịu trách nhiệm |

### Kết luận Phần A

**Nguyên nhân gốc**: [...]

**Tầng chính cần sửa**: [...]

**Vì sao cần 3 lớp giải pháp**:

- Lớp giao diện: [...]
- Lớp chỉ dẫn AI: [...]
- Lớp kiến trúc dữ liệu: [...]

---

## Phần B — Chọn định dạng demo

Mỗi lớp cần một bản demo. Demo giúp biến ý tưởng thành thứ trực quan để nhóm khác xem, kiểm tra và phản biện.

| Lớp | Thư mục | Định dạng demo chọn | Thời gian dự kiến |
|---|---|---|---|
| Giao diện | `1-uiux` | [vẽ tay / Excalidraw / Figma / HTML / ASCII / Mermaid] | __ phút |
| Chỉ dẫn AI | `2-prompt` | [bản prompt trong Markdown + ví dụ] | __ phút |
| Kiến trúc dữ liệu | `3-architecture` | [ASCII / Mermaid / sơ đồ hộp-mũi tên] | __ phút |

**Lý do chọn demo**

- Giao diện: [...]
- Chỉ dẫn AI: [...]
- Kiến trúc dữ liệu: [...]

Gợi ý: có thể dùng AI để dựng nhanh bản nháp demo, nhưng nhóm phải đọc lại và sửa.

### Chọn demo theo điều cần chứng minh

| Nếu cần chứng minh... | Demo phù hợp |
|---|---|
| Người dùng nhìn thấy gì | Sketch, Figma, HTML, ASCII UI |
| AI được chỉ dẫn thế nào | Bản prompt trong Markdown, ví dụ trả lời |
| Dữ liệu đi qua đâu | Sơ đồ hộp-mũi tên, ASCII, Mermaid |
| Quy trình chuyển sang người thật | Sơ đồ quy trình |

---

## Phần C — Ba lớp giải pháp

Ghi tóm tắt ở đây. Chi tiết nằm trong `card.md` và `demo.*` của từng thư mục.

### Lớp 1 — Giao diện (`artifact/1-uiux/`)

- **Cách tiếp cận**: Thêm disclaimer rõ ràng và nút "Chat với counselor" trên mọi câu trả lời liên quan đến eligibility/admission chances.
- **Hành động phòng vệ bao phủ**: Thông báo + Khắc phục
- **Demo**: ASCII mockup trong `artifact/1-uiux/demo.md`
- **Trạng thái**: Hoàn thành

Link chi tiết:

- `artifact/1-uiux/card.md`
- `artifact/1-uiux/demo.md`

### Lớp 2 — Chỉ dẫn AI (`artifact/2-prompt/`)

- **Cách tiếp cận**: Thêm rule bắt buộc trong system prompt: "Nếu user hỏi về eligibility/admission chances → từ chối trả lời và chuyển counselor".
- **Hành động phòng vệ bao phủ**: Ngăn + Từ chối + Chuyển người thật
- **Demo**: Full system prompt template trong `artifact/2-prompt/demo.md`
- **Trạng thái**: Hoàn thành

Link chi tiết:

- `artifact/2-prompt/card.md`
- `artifact/2-prompt/demo.md`

### Lớp 3 — Kiến trúc dữ liệu (`artifact/3-architecture/`)

- **Cách tiếp cận**: Thêm eligibility classifier module trước RAG pipeline. Nếu detect eligibility question → bypass RAG, directly escalate.
- **Hành động phòng vệ bao phủ**: Ngăn + Phát hiện + Khắc phục
- **Demo**: Mermaid flowchart trong `artifact/3-architecture/demo.md`
- **Trạng thái**: Hoàn thành

Link chi tiết:

- `artifact/3-architecture/card.md`
- `artifact/3-architecture/demo.md`

---

## Tổng kiểm tra

| Câu hỏi | Trả lời |
|---|---|
| Rủi ro chính đã chọn là gì? | **T-04** — Vượt thẩm quyền eligibility (AI tự đánh giá scholarship eligibility thay vì chuyển counselor) |
| Nguyên nhân gốc là gì? | Model được train "helpful" nên tự trả lời; thiếu explicit escalation rule; thiếu eligibility classifier; UI không cảnh báo limitation |
| 3 lớp giải pháp đã đủ chưa? | **Giao diện: ✅** (disclaimer + escalation button) / **Chỉ dẫn AI: ✅** (system prompt rule) / **Kiến trúc: ✅** (classifier + fallback) |
| 4 hành động đã bao phủ chưa? | **Ngăn: ✅** (classifier + prompt rule) / **Phát hiện: ✅** (trigger keywords) / **Khắc phục: ✅** (escalate to counselor) / **Thông báo: ✅** (disclaimer + offer ticket) |
| Nhóm khác đã góp ý chưa? | Chưa — nhóm chỉ có 2 người, tự rà lại |
| Nhóm đã sửa gì sau phản biện? | Đã thêm eligibility classifier vào architecture layer; đã chắc chắn trigger keywords; đã thêm audit log |

**Phản biện tự rà (4 câu):**

| Góc phản biện | Câu trả lời |
|---|---|
| **Đúng tầng** | ✅ Giải pháp map đúng nguyên nhân: UI (disclaimer), Prompt (rule), Architecture (classifier) |
| **Cụ thể** | ✅ Demo rõ: ASCII mockup UI, full system prompt, Mermaid flowchart + component table |
| **Đủ lớp** | ✅ 3 lớp bổ sung: UI là last line, Prompt buộc AI từ chối, Architecture block trước khi đến model |
| **Tác dụng phụ** | ⚠️ Có thể chậm thêm 100ms (classifier). Giảm bằng rule-based (không cần model). Alert khi knowledge base cũ (>30 ngày). |

## Phản biện chéo: 4 câu phải trả lời

Khi nhóm khác góp ý, hoặc khi nhóm tự rà lại, dùng 4 câu này:

| Góc phản biện | Câu hỏi |
|---|---|
| Đúng tầng | Giải pháp có sửa đúng nguyên nhân gốc không? |
| Cụ thể | Demo có đủ rõ để hiểu cách vận hành không? |
| Đủ lớp | 3 lớp có bổ sung cho nhau không, hay đang lặp cùng một ý? |
| Tác dụng phụ | Giải pháp có làm chậm, tốn kém, rối giao diện, hoặc gây hiểu nhầm mới không? |

Ghi góp ý cụ thể vào `card.md` hoặc phần tổng kiểm tra. Không ghi chung chung "ổn" hoặc "chưa ổn".

## Gợi ý chia việc

Nhóm 3 người:

- Thành viên A: `artifact/1-uiux/`
- Thành viên B: `artifact/2-prompt/`
- Thành viên C: `artifact/3-architecture/`

Nhóm 2 người:

- Một người phụ trách 2 lớp.
- Người còn lại phụ trách 1 lớp và rà lại 2 lớp kia.

5 phút cuối: cả nhóm đọc chéo 3 lớp, sửa lại bảng tổng kiểm tra, rồi chuẩn bị phản biện chéo.
