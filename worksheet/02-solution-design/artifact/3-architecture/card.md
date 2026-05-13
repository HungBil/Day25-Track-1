---
artifact: 3 — Lớp kiến trúc dữ liệu
bai-tap: 2 — Thiết kế giải pháp
demo: ./demo.md
---

# card.md — Lớp kiến trúc dữ liệu

**Tình huống xử lý**: T-04 (Vượt thẩm quyền eligibility)
Xem `../../1-map-and-format.md` Phần A.

---

## 1. Giải pháp là gì?

Thêm **Eligibility Classifier module** vào pipeline trước RAG:

```
User Question → Eligibility Classifier → (Yes) → Escalate to Counselor
                                   → (No)  → RAG Pipeline → Generate Answer
```

Classifier đánh giá câu hỏi có thuộc category "eligibility assessment" không, dựa trên:
- Intent detection (question type)
- Keyword matching (đủ điều kiện, có được không, khả năng, với điểm...)
- Entity extraction (có chứa điểm số, ngành, học bổng specific?)

Nếu classifier trả về "Yes" → bypass RAG, trả lời bằng canned response "Tôi không thể đánh giá..." và tạo ticket.

Nếu RAG không tìm thấy nguồn → fallback "Thông tin chưa có, vui lòng chat counselor."

---

## 2. Vì sao sửa ở lớp kiến trúc dữ liệu?

- **Nguyên nhân chính**: Thiếu module phân loại câu hỏi → model phải tự quyết định, dễ sai.
- **Cần kiểm tra dữ liệu trước khi câu trả lời được tạo ra**: Đảm bảo eligibility question không bao giờ được RAG xử lý.
- **Cần ghi lại lỗi để nhóm biết lỗi nào lặp lại nhiều**: Audit log cho mọi trường hợp từ chối.

**Hành động phòng vệ chính**:

- [x] Ngăn lỗi bằng classifier (block eligibility question trước khi đến model)
- [x] Phát hiện khi nguồn thiếu hoặc lỗi (RAG fallback)
- [x] Khắc phục bằng cách chuyển sang người thật (escalation ticket)
- [x] Ghi lại lỗi để cải thiện sau (audit log + monitoring dashboard)

---

## 3. Demo nằm ở đâu?

**File demo**: [`demo.md`](./demo.md)

Demo có:
- Mermaid flowchart thể hiện pipeline với classifier
- Component table với input/output/action cho mỗi thành phần
- Error handling table (nguồn thiếu, lỗi, out-of-scope)
- Monitoring dashboard mockup (real-time stats)
- Audit log schema (JSON example)

---

## 4. Tác dụng phụ

**Có thể gây vấn đề gì?**
- Trả lời chậm hơn vì thêm bước classifier.
- Phụ thuộc vào nguồn dữ liệu: nếu knowledge base lỗi thời, classifier có thể bỏ sót.
- Hệ thống phức tạp hơn, tốn công duy trì.

**Nhóm giảm vấn đề đó bằng cách nào?**
- Classifier là rule-based (keyword + regex) → nhanh, không cần model inference.
- Cache classifier result cho multi-turn conversation.
- Có alert khi knowledge base quá cũ (>30 ngày không cập nhật).
- Phân công 1 person duy trì classifier rules và knowledge base.

---

## 5. Checklist trước khi nộp

- [x] Sơ đồ cho thấy dữ liệu đi từ đâu đến đâu (User → Classifier → RAG/EScalate).
- [x] Có bước kiểm tra nguồn trước khi AI trả lời (classifier + RAG).
- [x] Có cách xử lý khi không có dữ liệu (fallback response + escalation).
- [x] Có cách chuyển sang người thật với tình huống rủi ro cao.
- [x] Có cách biết lỗi này có đang lặp lại không (audit log + monitoring).

**Người phụ trách**: Nguyễn Đông Hưng — 2A202600392
