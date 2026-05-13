---
artifact: 1 — Lớp giao diện
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp giao diện

**Tình huống xử lý**: T-04 (Vượt thẩm quyền eligibility)
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Khi chatbot trả lời về eligibility/admission chances/scholarship decision, giao diện hiển thị:
1. Disclaimer: "⚠️ Thông tin này chỉ tham khảo. Để được đánh giá chính xác, hãy chat với counselor."
2. Nút "Chat với counselor" nổi bật, dễ click.
3. Icon ⚠️ trước câu trả lời (nếu câu trả lời dựa trên knowledge base chứ không phải personal assessment).

**Mục đích**: Giúp user nhận biết câu trả lời không phải là đánh giá cá nhân, và có lối thoát nhanh để chuyển sang người thật.

---

## 2. Vì sao sửa ở lớp giao diện?

- Người dùng dễ tin câu trả lời của AI quá mức vì chatbot nằm trên website chính thức.
- Rủi ro xảy ra ở khoảnh khắc user đọc câu trả lời và hành động theo đó.
- Giao diện là lớp chặn cuối cùng (last line of defense) nếu prompt hoặc architecture lỏng lẻo.

**Hành động phòng vệ chính**:

- [x] Thông báo rõ giới hạn (AI không thể đánh giá eligibility)
- [x] Phát hiện dấu hiệu câu hỏi eligibility (trigger từ keywords)
- [x] Chuyển người thật qua nút button
- [x] Giúp người dùng kiểm tra lại nguồn chính thức

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:
- ASCII mockup chat bubble với disclaimer và button
- Trigger condition: User hỏi chứa keywords "đủ điều kiện", "có được không", "khả năng", "với điểm", "chắc"
- UX flow: User thấy disclaimer → click button → mở chat với counselor

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**
- Màn hình có thể rối hơn vì thêm icon và button.
- User có thể bỏ qua disclaimer và vẫn tin AI.

**Nhóm giảm vấn đề đó bằng cách nào?**
- Chỉ hiện disclaimer cho câu hỏi rủi ro cao (eligibility-related).
- Dùng icon ⚠️ nhỏ gọn, không làm gián đoạn.
- Đặt button "Chat với counselor" ở vị trí dễ click, có thể đóng nếu user không cần.

---

## 5. Checklist trước khi nộp

- [x] Giải pháp gắn đúng với rủi ro T-04 (AI tự đánh giá eligibility).
- [x] Demo nhìn vào là hiểu rủi ro đang được chặn ở đâu (disclaimer + escalation button).
- [x] Có đủ trạng thái bình thường và trạng thái lỗi (câu hỏi eligibility → hiển thị warning).
- [x] Có cách chuyển sang người thật khi AI không nên tự xử lý.
- [x] Câu chữ trong giao diện ngắn, không đổ hết trách nhiệm cho người dùng.

**Người phụ trách**: Quách Ngọc Quang — 2A202600285
