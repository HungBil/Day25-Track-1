---
artifact: 2 — Lớp chỉ dẫn AI
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp chỉ dẫn AI

**Tình huống xử lý**: T-04 (Vượt thẩm quyền eligibility)
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thêm rule bắt buộc vào system prompt:

**Khi user hỏi bất kỳ câu nào về eligibility, admission chances, approval decision, scholarship outcome → BẮT BUỘC trả lời bằng câu từ chối chuẩn và đề xuất chuyển counselor.**

Câu từ chối chuẩn:
"Tôi không thể đánh giá eligibility cá nhân. Hãy nộp hồ sơ qua [link] và counselor sẽ review trong 3-5 ngày. Tôi có thể tạo ticket #SC- giúp bạn."

Không được: đoán, đưa ra dự đoán, xác nhận theo giả định user, hay trả lời "có" / "không".

---

## 2. Vì sao sửa ở lớp chỉ dẫn AI?

- **AI đang trả lời quá tự tin khi thiếu nguồn**: Model được train để "helpful", nên có xu hướng trả lời mọi câu hỏi.
- **Cần luật rõ**: Khi nào trả lời, khi nào từ chối, khi nào chuyển sang người thật.
- **Có thể sửa nhanh** bằng prompt trước khi thay đổi hệ thống lớn hơn.

**Hành động phòng vệ chính**:

- [x] Ngăn câu trả lời sai ngay từ đầu (rule trong system prompt)
- [x] Bắt buộc nêu nguồn khi nói về thông tin quan trọng
- [x] Từ chối trả lời khi thiếu căn cứ
- [x] Chuyển người thật khi vượt phạm vi

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:
- Full system prompt template với rule mới
- Trigger keywords list
- Few-shot examples cho từng category
- Kết quả thử với 3 tình huống từ Bài 1 (T-04, T-20, T-21)

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**
- AI có thể từ chối quá nhiều, trở nên cứng nhắc.
- User cảm thấy không được hỗ trợ.

**Nhóm giảm vấn đề đó bằng cách nào?**
- Chỉ áp dụng rule với câu hỏi eligibility (có classifier hỗ trợ từ architecture layer).
- Câu từ chối đi kèm link hữu ích (hướng dẫn nộp hồ sơ) và offer tạo ticket → user cảm thấy được hỗ trợ dù bị từ chối.
- Test với bộ tình huống để điều chỉnh sensitivity.

---

## 5. Checklist trước khi nộp

- [x] Luật viết đủ cụ thể để AI làm theo (clear trigger + clear response).
- [x] Có mẫu câu khi AI không có đủ thông tin.
- [x] Có ví dụ cho tình huống dễ sai (T-04, T-20).
- [x] Có thử lại bằng tình huống trong Bài 1.
- [x] Không dùng prompt như cách duy nhất nếu lỗi nằm ở dữ liệu hoặc quy trình (có architecture layer bổ sung).

**Người phụ trách**: Nguyễn Đông Hưng — 2A202600392
