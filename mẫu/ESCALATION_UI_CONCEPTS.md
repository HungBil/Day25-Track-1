# 3 Ý Tưởng Escalation UI cho VinUni Admissions Chatbot
## Sketch Dạng ASCII + Interaction Flow

**Bối cảnh:** Chatbot AI đã trả lời câu hỏi nhưng không chắc chắn, hoặc user hỏi về thứ mà chatbot không được phép trả lời (ví dụ: xác nhận khả năng nhận học bổng). Cần rõ ràng escalate user đến thông tin chính thức / đội tư vấn viên.

---

## CONCEPT 1: "Confidence Level + Clear CTA" (Minimalist Trust-Based)
**Tone:** Clean, professional, no-nonsense. Show chatbot's confidence level transparently.

### Flow Diagram (ASCII)
```
┌─────────────────────────────────────────┐
│  Chat Window (Mobile/Desktop)           │
├─────────────────────────────────────────┤
│                                         │
│  User: "Tôi thi 24 điểm, có đủ         │
│         điều kiện học bổng không?"     │
│                                         │
│                                         │
│  🤖 Bot:                                │
│  "Mình không được phép xác nhận khả    │
│   năng nhận học bổng cụ thể vì nó      │
│   phụ thuộc vào hồ sơ riêng của bạn.   │
│                                         │
│   📋 TÙNG TRỌ CHÍNH THỨC 👇             │
│                                         │
│   🔗 Xem tiêu chí học bổng             │
│   🔗 Chat trực tiếp với tư vấn viên    │
│   📞 Gọi hotline: 024-xxxx-xxxx        │
│                                         │
│   ❓ Mình có thể giúp bạn được cái gì │
│      khác không?"                       │
│                                         │
└─────────────────────────────────────────┘
```

### Key Features:
- **Transparent refusal:** Chatbot rõ ràng nói "tôi không thể," không lẩn tránh
- **Three escalation paths:** (1) Official docs, (2) Live chat, (3) Hotline — user chọn
- **Positive reframe:** "Mình có thể giúp được cái gì khác không?" → keep engagement
- **No button confusion:** Simple links/buttons, dễ hiểu

### Design Details:
- Small icons (🔗 📞 🤖) để scan nhanh
- Text "TÙNG TRỢ CHÍNH THỨC" highlight (bold/color) để indicate "go here"
- Hotline number prominent (easily copied)
- Follow-up question warm & helpful

---

## CONCEPT 2: "Guided Escalation Modal" (Interactive, Step-by-Step)
**Tone:** Guided experience. Help user understand WHAT to do and WHY.

### Flow Diagram (ASCII)
```
┌────────────────────────────────────────┐
│  POPUP MODAL (Overlay on Chat)         │
├────────────────────────────────────────┤
│                                        │
│  🛑 VinUni Chưa Có Thông Tin Đầy Đủ  │
│                                        │
│  "Câu hỏi của bạn liên quan đến      │
│   tính chất riêng của hồ sơ. Mình     │
│   cần kết nối bạn với tư vấn viên    │
│   để được hỗ trợ tốt nhất."           │
│                                        │
│  ┌──────────────────────────────────┐ │
│  │ BƯỚC 1: Chọn hình thức liên hệ   │ │
│  ├──────────────────────────────────┤ │
│  │ ○ Chat trực tiếp (5 phút reply)  │ │
│  │ ○ Gọi hotline (sẵn sàng 24/7)    │ │
│  │ ○ Lịch tư vấn (1-1 meeting)      │ │
│  └──────────────────────────────────┘ │
│                                        │
│  ┌──────────────────────────────────┐ │
│  │ BƯỚC 2: Thông tin liên hệ        │ │
│  ├──────────────────────────────────┤ │
│  │ Tên: [_________________]         │ │
│  │ Email: [_________________]       │ │
│  │ Số điện thoại: [_____________]   │ │
│  └──────────────────────────────────┘ │
│                                        │
│  ┌──────────────────────────────────┐ │
│  │ BƯỚC 3: Lưu yêu cầu              │ │
│  │                                  │ │
│  │ [Quay lại Chat] [Tiếp tục >]     │ │
│  └──────────────────────────────────┘ │
│                                        │
└────────────────────────────────────────┘
```

### Key Features:
- **Step-by-step wizard:** Reduces decision fatigue
- **Transparency on wait time:** "5 phút reply" → set expectations
- **Multiple options:** User feels in control (not forced into single path)
- **Data capture:** Collect contact info so counselor can follow up
- **Reversible:** "Quay lại Chat" — not pushy

### Design Details:
- Red/orange icon (🛑) shows this is escalation (not normal chat)
- Radio buttons for method selection
- Form fields minimal (only essential info)
- Button hierarchy: secondary "Quay lại" vs primary "Tiếp tục"
- Progress indicator implied (BƯỚC 1, 2, 3)

---

## CONCEPT 3: "Smart Detection + Soft Escalation" (Ambient, Non-Intrusive)
**Tone:** Anticipatory. System proactively recognizes uncertainty and gently offers help.

### Flow Diagram (ASCII)
```
┌──────────────────────────────────────────┐
│  Chat Conversation                       │
├──────────────────────────────────────────┤
│                                          │
│  User: "Con em thi 24 điểm, nộp hồ sơ  │
│         cho ngành CS, có cơ hội không?" │
│                                          │
│  🤖 Bot: "Con em có lẽ có cơ hội. Tuy  │
│     nhiên, xác nhận chính thức phụ      │
│     thuộc vào toàn bộ hồ sơ."           │
│                                          │
│     ⚠️ CONFIDENCE: Thấp (60%)            │
│     ► Nghe tư vấn viên chuyên về CS    │
│       (Tôi không chắc 100%)             │
│                                          │
│     [📞 Chat với tư vấn viên]            │
│                                          │
└──────────────────────────────────────────┘
```

### Key Features:
- **Confidence meter visible:** "Thấp (60%)" → builds trust by showing uncertainty
- **Reason disclosed:** "Tôi không chắc 100%" → honest about limitation
- **Soft escalation button:** Appears inline, not modal (less disruptive)
- **Specialist suggestion:** "Nghe tư vấn viên chuyên về CS" → give context for escalation
- **Keep original answer:** Bot still answered, but transparency about doubt

### Design Details:
- Inline confidence badge (⚠️ symbol) subtle but visible
- Button color: accent color (blue/green), not alarm red
- Text tone: "có lẽ" (maybe) instead of confident assertion
- Single clear CTA (not overloading with 3 options)
- Confidence color coding possible: 🟢 (high >80%), 🟡 (medium 50-80%), 🔴 (low <50%)

---

## Detailed Interaction Flows

### Flow A: User Initiates Escalation

```
User asks eligibility question
        ↓
Chat processes intent
        ↓
   ┌─► CONFIDENT (>80%): Answer normally
   │
   ├─► MEDIUM (50-80%): Answer + soft escalation button
   │
   └─► LOW (<50%) OR RESTRICTED TOPIC:
       
       Chatbot: "Tôi không được phép..."
       
       Show clear escalation CTA:
       - Links to official docs
       - Chat/hotline/booking button
       - Warm follow-up offer
       
       Escalation logged:
       └─► Timestamp: YYYY-MM-DD HH:MM
       └─► User ID: xxxx
       └─► Question: "..."
       └─► Escalation method: chat|hotline|booking
       └─► Counselor assigned: [Auto-route to specialist]
```

### Flow B: Proactive Detection (System Senses Distress)

```
User message analyzed
        ↓
   System detects:
   - Urgent language ("hôm nay", "gấp")
   - Stress signals ("lo", "sợ", "chết")
   - Eligibility questions (restricted topic)
        ↓
   IF (urgent OR stress) AND (no escalation yet):
   
   → Auto-show soft escalation banner
     "Nghe tôi, bạn có vẻ cần tư vấn ngay.
      Hãy nói chuyện với tư vấn viên."
   
   → Button: [Kết nối ngay]
   
   → If still no click, send gentle reminder
     after 30 seconds:
     "Em còn ở đây nếu cần giúp đỡ thêm"
     
   → Log for counselor:
     ├─ Stress signal detected: "lo"
     ├─ Time: 14:32
     ├─ Context: "Con tôi lo là không đủ điểm"
     └─ Action: Proactive escalation suggested
```

---

## Technical Notes for Implementation

### Data to Log Every Escalation

```json
{
  "escalation_id": "esc_20260513_001",
  "timestamp": "2026-05-13T14:32:00Z",
  "user_id": "user_12345",
  "user_name": "Nguyễn Văn A",
  "user_contact": {
    "email": "a@example.com",
    "phone": "0976xxx"
  },
  "trigger_type": "confidence_low" | "restricted_topic" | "distress_signal" | "user_initiated",
  "original_question": "Con em thi 24 điểm, có đủ điều kiện học bổng không?",
  "confidence_score": 0.42,
  "escalation_method": "chat" | "hotline" | "booking",
  "assigned_counselor": "counselor_id_123",
  "status": "pending" | "in_progress" | "resolved",
  "resolution_time_minutes": 5,
  "notes": "Student expressed urgency; low confidence in scholarship eligibility criteria"
}
```

### Guardrails to Prevent Misuse

1. **4-hour SLA:** Escalation must be acknowledged within 4 hours (per VinUni policy)
2. **No refusal:** Chatbot can NEVER refuse to escalate; it can only offer additional escalation methods
3. **Confidence threshold:** Automatically escalate if confidence < 50%
4. **Restricted topics whitelist:** Define which topics require human escalation
   - Scholarship eligibility ✓
   - Admission chances ✓
   - Financial aid details ✓
   - Emotional support ✓
   - General info (programs, fees) ✗ (can answer)
5. **Escalation visibility:** Button/link must be visible within 2 seconds of page scroll (not buried)

---

## Comparison: Which Concept for VinUni?

| Concept | Best For | Pros | Cons |
|---------|----------|------|------|
| **#1: Confidence + CTA** | Initial launch, all user types | Simple, clear, fast | Less sophisticated; doesn't guide user to best channel |
| **#2: Guided Modal** | Capturing user intent & contact info | Streamlined escalation; data collection; professional feel | Takes up screen; can feel intrusive if user just wants answer |
| **#3: Smart Detection** | Mature product with good intent models | Non-intrusive; proactive; builds trust via transparency | Requires good ML intent detection; false positives frustrate users |

### Recommendation: Hybrid Approach
- **Day 1:** Use Concept #1 (Confidence + CTA) — easy to implement, works immediately
- **Month 2:** Add Concept #3 detection (Smart Detection) for proactive escalation
- **Month 3:** Integrate Concept #2 modal for high-intent users who explicitly click escalation button

---

## Example Restricted Topics (Policy)

```
CHATBOT CAN ANSWER:
✓ "Ngành CS có học phí bao nhiêu?"
✓ "Deadline nộp hồ sơ khi nào?"
✓ "Tôi cần chuẩn bị giấy tờ gì?"
✓ "Có học bổng nào cho sinh viên khó khăn?"

CHATBOT MUST ESCALATE:
✗ "Con em có đủ điều kiện học bổng không?"
✗ "Con em có cơ hội vào trường không?"
✗ "Học bổng này em có thể nhận không?"
✗ "Tôi rất lo sợ không được nhận, phải làm sao?"
✗ "Em đang có tâm lý áp lực, ai có thể nghe tôi?"
```

---

## Next Steps

1. **Choose design direction** (or hybrid of 2-3)
2. **Build interactive prototype** (HTML/React)
3. **Test with real users** (HS 17-18, parents 40-55)
4. **Refine escalation SLA** (ensure 4-hour counselor response)
5. **Implement logging/monitoring** dashboard for counselors
6. **Train counselors** on how to handle escalated chats (tone, first response timing, etc.)

---

*Prepared for: VinUni Chatbot UI Design Workshop*  
*Date: May 13, 2026*
