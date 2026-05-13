---
artifact: 1 — Demo giao diện
format: ASCII mockup chat bubbles
---

# demo.md — Demo giao diện

File này minh họa cách giao diện hiển thị disclaimer và nút escalation cho câu hỏi eligibility.

---

## 1. Sơ đồ chat flow

```text
User hỏi về eligibility/admission chances
    ↓
System phát hiện trigger keywords
    ↓
Hiển thị chat bubble với ⚠️ + disclaimer + button
    ↓
User click "Chat với counselor"
    ↓
Mở chat window với counselor (hoặc tạo ticket)
```

---

## 2. ASCII Mockup

### Trường hợp 1: User hỏi về eligibility

```text
┌─────────────────────────────────────────────────────────────┐
│  User: Con thi 24 điểm, học ở Hà Nội, có đủ điều kiện      │
│        nhận học bổng Merit 100% không?                    │
├─────────────────────────────────────────────────────────────┤
│  Bot: ⚠️ Thông tin này chỉ tham khảo. Tôi không thể       │
│       đánh giá eligibility cá nhân.                       │
│                                                           │
│       [Xem tiêu chí học bổng Merit 100%]                 │
│       [💬 Chat với counselor]  ← nút nổi bật              │
└─────────────────────────────────────────────────────────────┘
```

### Trường hợp 2: User hỏi thông tin thông thường (deadline)

```text
┌─────────────────────────────────────────────────────────────┐
│  User: Deadline học bổng toàn phần CNTT là ngày nào?     │
├─────────────────────────────────────────────────────────────┤
│  Bot: Hạn nộp học bổng toàn phần ngành CNTT năm 2026 là  │
│       31/03/2026.                                         │
│       Nguồn: [Link trang học bổng chính thức]            │
│                                                           │
│       [Chat với counselor]  ← nhỏ, không nổi bật         │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. Trigger condition

Trigger disclaimer khi user hỏi chứa **ít nhất một** keyword:

| Category | Keywords (Vietnamese) |
|---|---|
| Eligibility | "đủ điều kiện", "có đủ", "đủ không", "được không" |
| Admission chances | "có khả năng", "khả năng cao", "với điểm này", "với điểm như em" |
| Decision certainty | "chắc không", "chắc chắn", "có nên", "nên nộp" |
| Scholarship approval | "nhận học bổng", "được học bổng", "cơ hội học bổng" |

---

## 4. UX flow

1. User nhập câu hỏi → System detect keywords.
2. Nếu question type = "eligibility assessment" → hiển thị disclaimer + button.
3. Nếu question type = "general info" → không hiển thị disclaimer (hoặc chỉ hiện icon nhỏ).
4. Button "Chat với counselor" click → mở chat window với counselor OR tạo ticket và thông báo "Ticket #SC-XXXX đã được tạo. Counselor sẽ phản hồi trong 3-5 ngày."

---

## 5. Checklist demo

- [x] Mockup rõ disclaimer và button.
- [x] Trigger condition được định nghĩa.
- [x] Hai trạng thái: eligibility question vs general info.
- [x] UX flow từ question đến escalation rõ ràng.
- [x] Câu chữ ngắn, dễ đọc trên mobile.
