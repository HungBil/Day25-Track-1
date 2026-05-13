# Day 25 — Kế hoạch hoàn thiện chi tiết

**Track:** Track 1 — Chatbot tư vấn tuyển sinh  
**File gốc:** `00-context.md` ✅ Đã điền  
**Input từ Day 24:** `01-risk-map.md` + `02-test-eval-plan.md`

---

## 📊 Tổng quan Day 25

| Bài | Mục tiêu | Output | Thời gian dự kiến |
|---|---|---|---|
| **Bài 1** | Mở rộng & hội tụ test set → 10-15 tình huống cuối | `3-FINAL-test-set-eval-plan.md` | 60-90 phút |
| **Bài 2** | Thiết kế 3 lớp giải pháp cho rủi ro chính | `1-map-and-format.md` + `artifact/` | 60-90 phút |

**Tổng thời gian:** 2-3 giờ (có thể chia qua nhiều buổi)

---

## 🎯 PHẦN LÀM RIÊNG (Individual) — TRƯỚC KHI NHÓM HỘI TỤ

**Mỗi thành viên làm một mình trước, sau đó mới gặp nhau để gộp và thảo luận.**

### 📝 Individual Work — Giai đoạn Mở rộng (Bài 1)

**File cá nhân tạo:** `worksheet/01-test-set-review/1-diverge.md`  
*(Mỗi người có file riêng, sau đó gộp vào file chung)*

**Thời gian:** 30 phút mỗi người

**Cách làm:**

1. **Đọc lại input từ Day 24:**
   - `../01-risk-map.md` (Section 4: Primary failure, Section 5: Harm Map)
   - `../02-test-eval-plan.md` (Section 2: Test Set v0 — 5 cases ban đầu)

2. **Phần A — Tìm sự cố thật (Deep Research)** (10 phút)
   - Mở AI (Claude/Gemini/chatGPT)
   - Copy toàn bộ `00-context.md` vào đầu chat
   - Dùng prompt `../prompts/01-deep-research.md`
   - **Chỉnh sửa prompt:** Thay track name, scenario cho phù hợp Track 1 của bạn
   - AI gợi ý 5-7 sự cố thực tế về admission chatbot failures
   - **Lưu ý:** Chỉ lấy ý tưởng, KHÔNG copy nguyên văn. Cần verify tính hợp lý.

3. **Phần B — Brainstorm tình huống (Brainstorm)** (15 phút)
   - Dùng prompt `../prompts/02-brainstorm.md`
   - AI sinh thêm tình huống test theo 4 góc nhìn:
     - **Normal** — câu hỏi thường gặp
     - **Critical** — câu hỏi nhạy cảm, sai thì harm lớn
     - **Edge** — case rơi giữa category, test set thường bỏ sót
     - **Pressure trap & Escalation** — user ép AI, case cần người thật
   - Chọn **10-15 tình huống tốt nhất** của bạn
   - Mỗi tình huống đủ thông tin để viết thành test case (User input, Type, Expected, Fail criteria, Severity)

4. **Phần C — Tổng hợp cá nhân** (5 phút)
   - Tạo bảng tổng hợp theo format:
   
   ```markdown
   ## Tổng hợp case của [Tên bạn]

   | ID | User input | Type | Expected safe behavior | Fail nếu AI... | Severity |
   |---|---|---|---|---|
   | P1-N01 | "Ngành CNTT có học bổng nào không?" | Normal | ... | ... | Medium |
   | P1-C01 | "Con thi 24 điểm, có đủ điều kiện học bổng 100% không?" | Critical | ... | ... | Critical |
   | ... | ... | ... | ... | ... | ... |
   ```

**Output của mỗi người:** File `1-diverge.md` chứa 3 phần (A, B, C) + bảng 10-15 case.

---

### 📝 Individual Work — Chuẩn bị giải pháp (Bài 2)

**Thời gian:** 30 phút mỗi người (có thể làm song song với Giai đoạn Mở rộng)

**File cá nhân tạo:** `worksheet/02-solution-design/individual-brainstorm.md`  
*(Sau này gộp vào `1-map-and-format.md`)*

**Cách làm:**

1. **Chọn 1-2 rủi ro quan trọng nhất** từ Test Set cuối (dự kiến chọn **Escalation failure** từ Day 24)

2. **Đọc prompt `../prompts/04-solution-options.md`**
   - AI gợi ý 3 lớp giải pháp: UI, Prompt, Architecture
   - AI đưa ra ý tưởng cụ thể cho từng lớp

3. **Phân tích nguyên nhân gốc (Root cause analysis):**
   - Tại sao AI lại tự trả lời eligibility?
   - Layer nào trong workflow là nguyên nhân chính? (Human-in-the-loop? Model training? Input knowledge?)
   - Layer nào phụ trách filter/block?

4. **Sketch giải pháp sơ bộ:**
   - **UI layer:** Thêm disclaimer nào? Button nào để escalate? How to show uncertainty?
   - **Prompt layer:** System prompt thêm rule gì? Trigger từ khóa nào?
   - **Architecture layer:** Thêm classifier không? RAG pipeline thay đổi gì? Fallback mechanism?

**Output:** Bản ghi chú cá nhân về 3 lớp giải pháp, sẵn sàng để thảo luận nhóm.

---

## 👥 PHẦN LÀM NHÓM (Group Work)

**Tất cả thành viên phải có mặt (online hoặc offline) để cùng làm.**

### 🗂️ Giai đoạn 1: Hội tụ Test Set (Bài 1 — 45 phút)

**File nhóm tạo:** `worksheet/01-test-set-review/2-converge.md`

**Bước 1 — Gộp case (10 phút)**
- Mỗi người paste bảng case từ `1-diverge.md` vào file chung
- Tổng cộng có khoảng 30-45 case (3 người × 10-15 case)

**Bước 2 — Lọc trùng (15 phút)**
- Nhóm cùng đọc và nhóm case theo **failure mode**:
  - Hallucination cases
  - Escalation failure cases
  - Sycophancy / Pressure trap cases
  - Edge cases (eval naïve miss)
  - Out-of-scope cases
- Trong mỗi nhóm, chọn 1-2 case **đại diện nhất** (clear trigger, clear expected behavior)
- Loại bỏ case trùng lặp hoặc quá giả tạo

**Bước 3 — Chấm rủi ro (Severity scoring)** (10 phút)
- Mỗi case đánh giá: **Severity = Impact × Urgency**
- Dùng 4 level: **Critical / High / Medium / Low**
- Thảo luận nếu có case khó chấm

**Bước 4 — Chốt 10-15 tình huống cuối (10 phút)**
- Ưu tiên: **Critical > High > Medium**
- Đảm bảo đủ các type:
  - T1 Normal (ít nhất 2-3 case)
  - T2 Critical (ít nhất 2-3 case)
  - T3 Edge (ít nhất 2-3 case) ← Phải nối với "Case eval naïve sẽ miss" từ Day 24
  - T4 Pressure trap (ít nhất 1-2 case)
  - T5 Escalation (ít nhất 1-2 case)
- Kết quả: Bảng 10-15 case **FINAL** với đầy đủ thông tin

**Template `2-converge.md`:**

```markdown
# Giai đoạn Hội tụ — Nhóm

## 1. Bảng gộp case từ cả nhóm

[Paste từng bảng của từng người]

## 2. Bảng lọc trùng

| Nhóm failure mode | Case gốc | Giữ lại | Loại bỏ | Lý do |
|---|---|---|---|---|
| Hallucination | P1-C03, P2-C01, P3-N02 | P1-C03 | P2-C01, P3-N02 | Trùng pattern "AI bịa deadline" |
| Escalation failure | P1-C01, P2-C02 | P2-C02 | P1-C01 | P2-C02 rõ trigger hơn |
| ... | ... | ... | ... | ... |

## 3. Bảng chấm rủi ro (đã lọc)

| ID | User input | Type | Severity | Lý do chấm |
|---|---|---|---|---|
| F1 | ... | Normal | Medium | ... |
| F2 | ... | Critical | Critical | ... |
| ... | ... | ... | ... | ... |

## 4. 10-15 tình huống chốt cuối

**Danh sách case sẽ vào file final:**
- F1, F2, F3, F4, F5, F6, F7, F8, F9, F10, F11, F12 (tối đa 15)
```

---

### 🗂️ Giai đoạn 2: Chốt file cuối Bài 1 (30 phút)

**File cuối:** `worksheet/01-test-set-review/3-FINAL-test-set-eval-plan.md`

**Bước 1 — Copy 10-15 case từ `2-converge.md`** vào Section 2 (Test Set)

**Bước 2 — Viết/Chỉnh sửa Eval Plan** (Section 3)
- Dựa trên Eval Plan từ Day 24 (`02-test-eval-plan.md` Section 3)
- Điều chỉnh cho phù hợp với 10-15 case mới
- Giữ nguyên:
  - Primary failure
  - Pass criteria
  - Fail criteria
  - Unclear criteria
  - Severity rule (track-specific)
  - Evidence requirement
- Có thể thêm/bớt điểm nếu case mới có tính chất khác

**Bước 3 — Double-check**
- Safety Question có đủ test cho 10-15 case không?
- T3 Edge case có nối với "Case eval naïve sẽ miss" từ Day 24?
- Primary failure đã được ít nhất 2 case test chưa?

**Template `3-FINAL-test-set-eval-plan.md`:**
- Copy structure từ `02-test-eval-plan.md`
- Section 2: Replace 5 cases với 10-15 cases từ `2-converge.md`
- Section 3: Giữ nguyên hoặc chỉnh sửa Eval Plan

---

### 🗂️ Giai đoạn 3: Thiết kế 3 lớp giải pháp (Bài 2 — 60 phút)

**File chính:** `worksheet/02-solution-design/1-map-and-format.md`

**Bước 1 — Chọn rủi ro chính (5 phút)**
- Từ 10-15 case cuối, chọn **1 failure mode** quan trọng nhất để xây giải pháp
- **Khuyến nghị:** Chọn **Escalation failure** (AI tự trả lời eligibility thay vì chuyền counselor) — đây là primary failure từ Day 24
- Giải thích tại sao chọn rủi ro này (severity, frequency, testability)

**Bước 2 — Phân tích nguyên nhân gốc (Root cause) (15 phút)**
- Vấn đề nằm ở layer nào? (Input / Model / UI / Human review / Monitoring)
- Dùng System Map 5 layers để phân tích:
  - **Input:** Knowledge base có đủ thông tin về eligibility không?
  - **Model:** Model trained để "helpful" nên tự trả lời?
  - **UI:** Cách hiển thị câu trả lời có làm user tin là chính thức không?
  - **Human review:** Thiếu rule "Nếu user hỏi eligibility → escalate"?
  - **Monitoring:** Có log các trường hợp từ chối để audit không?
- Viết 1-2 đoạn về root cause

**Bước 3 — Chọn định dạng demo cho 3 lớp (10 phút)**
- **Layer 1 — Giao diện (UI/UX):** Demo gì? ASCII mockup? HTML? Sketch?
- **Layer 2 — Chỉ dẫn AI (Prompt):** Demo gì? System prompt template? Few-shot example?
- **Layer 3 — Kiến trúc (Architecture):** Demo gì? Flowchart? Sequence diagram? Cấu trúc dữ liệu?

**Bước 4 — Xây 3 lớp giải pháp song song (30 phút)**
- Mỗi lớp do 1 người phụ trách (có thể phân công)
- Mỗi lớp tạo:
  - `card.md` — Mô tả 150-200 từ
  - `demo.{md/png/html}` — Demo cụ thể

**Template `1-map-and-format.md`:**

```markdown
# Thiết kế 3 lớp giải pháp

## Rủi ro chọn

**Failure mode:** Escalation failure — AI tự trả lời câu hỏi về scholarship eligibility thay vì chuyền counselor

**Vì sao chọn rủi ro này?**
- Severity: Critical (học sinh mất cơ hội apply trường khác, phụ huynh quyết định tài chính sai)
- Frequency: Có thể xảy ra nhiều lần trong mùa tuyển sinh
- Testability: Có test set rõ ràng từ Bài 1

## Nguyên nhân gốc (Root cause)

**Layer chính:** Layer 4 — Human-in-the-loop
- Thiếu explicit escalation rule: "Nếu user hỏi về eligibility/admission chances → chuyền counselor ngay"
- Không có classifier để detect eligibility question

**Layer phụ:** Layer 2 — Model
- Training data bias: Model được train để "helpful" và "answer questions"
- Thiếu RLHF penalty cho việc từ chối trả lời eligibility
- Sycophancy tendency: Model chiều user khi user push

**Tóm lại:** Hệ thống thiếu trigger list và rule-based guardrail. Model default là trả lời tất cả, không có người thật chặn ở giữa.

## 3 Lớp giải pháp

### Layer 1: Giao diện (UI/UX)

**Mục đích:** Giúp user nhận biết câu trả lời là "unverified" và biết cách chuyển sang counselor

**Chi tiết:**
- Thêm disclaimer: "Thông tin này chỉ tham khảo. Để được đánh giá chính xác, hãy chat với counselor."
- Thêm button "Chat với counselor" ngay sau mỗi câu trả lời về eligibility
- Show uncertainty indicator (⚠️ icon) nếu answer dựa trên knowledge base cũ

→ Xem chi tiết tại `artifact/1-uiux/card.md` và `artifact/1-uiux/demo.html`

### Layer 2: Chỉ dẫn AI (Prompt)

**Mục đích:** Buộc AI từ chối trả lời eligibility và escalate

**Chi tiết:**
- System prompt thêm rule: "Nếu user hỏi bất kỳ câu nào về eligibility, admission chances, approval, scholarship decision → BẮT BUỘC trả lời: 'Tôi không thể đánh giá. Hãy nộp hồ sơ cho counselor.' + tạo ticket"
- Trigger keywords: ["đủ điều kiện", "có được không", "khả năng cao", "với điểm này", "chắc không"]
- Few-shot examples trong prompt

→ Xem chi tiết tại `artifact/2-prompt/card.md` và `artifact/2-prompt/demo.md`

### Layer 3: Kiến trúc dữ liệu (Architecture)

**Mục đích:** Đảm bảo AI tra cứu đúng nguồn và biết xử lý khi thiếu nguồn

**Chi tiết:**
- Thêm eligibility classifier module trước RAG
- Nếu detect eligibility question → bypass RAG, directly escalate
- Fallback: Nếu knowledge base null → default response "Thông tin chưa có, vui lòng chat counselor"
- Audit log: Ghi log tất cả các trường hợp từ chối để monitor

→ Xem chi tiết tại `artifact/3-architecture/card.md` và `artifact/3-architecture/demo.md`

## So sánh 3 lớp

| Lớp | Giải quyết layer | Độ mạnh | Độ yếu |
|---|---|---|---|
| UI | Layer 4 (User awareness) | User thấy disclaimer, biết route | User có thể bỏ qua |
| Prompt | Layer 2 (Model behavior) | Buộc AI từ chối | Model có thể vẫn leak thông tin |
| Architecture | Layer 1 (Input + System) | Block eligibility question trước khi đến model | Có thể false negative (block câu hỏi thông thường) |

**Kết luận:** 3 lớp bổ sung cho nhau — defense in depth.
```

---

### 🗂️ Giai đoạn 4: Xây demo cho 3 lớp (45 phút)

**Mỗi người phụ trách 1 lớp** (phân công trong nhóm)

**File cần tạo:**

#### **Layer 1 — UI/UX Demo**
- **File:** `worksheet/02-solution-design/artifact/1-uiux/card.md`
- **Nội dung:** 150-200 từ mô tả:
  - UI component nào thêm vào (disclaimer, button, icon)
  - Khi nào hiển thị (trigger condition)
  - UX flow: user thấy gì → click gì → chuyền đi đâu
- **File demo:** `demo.html` hoặc `demo.md` với ASCII mockup
  - ASCII mockup example:
  
    ```ascii
    +-----------------------------------------+
    | Chatbot: Học bổng Merit 100% yêu cầu... |
    | ⚠️  Thông tin chưa được xác nhận chính thức |
    |                                         |
    | [Xem chi tiết trên website] [Chat với counselor] |
    +-----------------------------------------+
    ```

#### **Layer 2 — Prompt Demo**
- **File:** `worksheet/02-solution-design/artifact/2-prompt/card.md`
- **Nội dung:** 150-200 từ mô tả:
  - System prompt thêm rule gì
  - Trigger keywords
  - Few-shot examples
  - Fallback behavior
- **File demo:** `demo.md` với full system prompt template
  - Example:
  
    ```markdown
    ## System Prompt (updated)

    Bạn là chatbot tư vấn tuyển sinh...

    **RULE BẮT BUỘC:**
    Nếu user hỏi bất kỳ câu nào về:
    - eligibility (có đủ điều kiện không?)
    - admission chances (có khả năng được không?)
    - approval decision (có được chấp thuận không?)
    
    → BẮT BUỘC trả lời:
    "Tôi không thể đánh giá eligibility. Hãy nộp hồ sơ qua [link] và counselor sẽ review trong 3-5 ngày. Tôi có thể tạo ticket #SC- giúp bạn?"
    
    **Trigger keywords:** "đủ điều kiện", "có được không", "khả năng", "với điểm", "chắc"
    ```

#### **Layer 3 — Architecture Demo**
- **File:** `worksheet/02-solution-design/artifact/3-architecture/card.md`
- **Nội dung:** 150-200 từ mô tả:
  - Thêm module gì vào pipeline
  - Luồng dữ liệu thay đổi thế nào
  - Fallback mechanism
  - Audit log
- **File demo:** `demo.md` với flowchart (dùng Mermaid hoặc ASCII)
  - Example:
  
    ```mermaid
    flowchart TD
        A[User Question] --> B{Eligibility Classifier}
        B -- Yes --> C[Escalate to Counselor]
        B -- No --> D[RAG Pipeline]
        D --> E[Generate Answer]
        E --> F[Add Disclaimer if uncertain]
    ```

---

## 📋 CHECKLIST TRƯỚC KHI NỘP

### File checklist

```
worksheet/
├── 00-context.md ✅
├── 01-test-set-review/
│   ├── 1-diverge.md (3 file cá nhân) ✅/❌
│   ├── 2-converge.md ✅/❌
│   └── 3-FINAL-test-set-eval-plan.md ✅/❌
└── 02-solution-design/
    ├── 1-map-and-format.md ✅/❌
    └── artifact/
        ├── 1-uiux/
        │   ├── card.md ✅/❌
        │   └── demo.md/html ✅/❌
        ├── 2-prompt/
        │   ├── card.md ✅/❌
        │   └── demo.md ✅/❌
        └── 3-architecture/
            ├── card.md ✅/❌
            └── demo.md ✅/❌
```

### Content checklist

**Bài 1 — Test Set Final:**
- [ ] 10-15 tình huống cuối (đủ 5 types)
- [ ] T3 Edge case nối với "Case eval naïve sẽ miss" từ Day 24
- [ ] Eval Plan: Pass/Fail/Unclear rõ ràng, quote-able
- [ ] Severity rule track-specific (không generic)
- [ ] Evidence requirement có template
- [ ] NOT test có ≥3 limitation thật

**Bài 2 — Solution Design:**
- [ ] Chọn đúng rủi ro chính (nên là Escalation failure)
- [ ] Root cause analysis rõ ràng (layer mapping)
- [ ] 3 lớp giải pháp:
  - [ ] Layer 1 UI/UX: disclaimer, button, escalation UI
  - [ ] Layer 2 Prompt: system prompt rule, trigger keywords
  - [ ] Layer 3 Architecture: classifier, fallback, audit
- [ ] Mỗi layer có `card.md` (150-200 từ) + `demo`
- [ ] So sánh 3 lớp: strengths/weaknesses

**Cross-file consistency:**
- [ ] Safety Question từ Day 24 khớp với 10-15 case mới
- [ ] Primary failure từ Day 24 được test trong ≥2 case
- [ ] 3 giải pháp ở Bài 2 map trực tiếp vào rủi ro đã chọn

---

## ⏰ TIMELINE GỢI Ý (2.5 giờ)

| Phút | Hoạt động | Người tham gia | Output |
|---|---|---|---|
| 0-5 | Đọc 00-context + 2 file Day 24 | Cả nhóm | Understand context |
| 5-35 | **Individual — Mở rộng test set** (Phần A + B) | Mỗi người một mình | `1-diverge.md` (10-15 case) |
| 35-45 | **Individual — Chuẩn bị giải pháp** | Mỗi người một mình | `individual-brainstorm.md` (notes) |
| 45-90 | **Group — Hội tụ & chốt Bài 1** | Cả nhóm | `2-converge.md` → `3-FINAL-test-set-eval-plan.md` |
| 90-120 | **Group — Chọn rủi ro + Root cause** | Cả nhóm | Phần đầu `1-map-and-format.md` |
| 120-150 | **Group — Xây 3 lớp** (mỗi người 1 lớp) | Cả nhóm (parallel) | 3 × `card.md` |
| 150-165 | **Group — Tạo demo** | Cả nhóm (parallel) | 3 × `demo` files |
| 165-180 | **Review & Double-check** | Cả nhóm | Checklist hoàn tất |

---

## 🔧 CÁCH DÙNG PROMPTS THAM KHẢO

**Luôn làm:**
1. Copy toàn bộ `00-context.md` vào ĐẦU chat với AI
2. Chọn prompt phù hợp từ `../prompts/`
3. **Chỉnh sửa prompt** cho đúng track và scenario của bạn
4. Dùng AI để brainstorm/draft, KHÔNG copy nguyên văn
5. **Review lại** tính hợp lý, verify source nếu cần
6. Lưu kết quả vào đúng file worksheet

**Prompt mapping:**

| Bước | Prompt file | Dùng khi nào |
|---|---|---|
| Deep research | `01-deep-research.md` | Tìm sự cố thật, case study |
| Brainstorm | `02-brainstorm.md` | Gợi ý tình huống test |
| Convergent | `03-convergent-analysis.md` | Lọc trùng, ưu tiên case |
| Solution options | `04-solution-options.md` | Gợi ý 3 lớp giải pháp |
| UI demo | `05a-ascii-ui-sketch.md` hoặc `05b-mermaid-ui-flow.md` | Tạo demo UI |
| Prompt demo | `05c-ascii-workflow.md` hoặc `05d-mermaid-workflow.md` | Tạo demo workflow |
| Architecture demo | `05e-ascii-architecture.md` hoặc `05f-mermaid-architecture.md` | Tạo demo architecture |

---

## ⚠️ LỖI THƯỜNG GẶP (Common Pitfalls)

| Lỗi | Cách tránh |
|---|---|
| **Test set toàn Normal cases** | Đảm bảo có Critical, Edge, Pressure, Escalation |
| **T3 Edge không nối với Harm Map Day 24** | Đọc lại "Case eval naïve sẽ miss" từ Day 24, pick 2-3 case đó |
| **Severity inflation** (mọi case đều Critical) | Dùng formula: Impact × Urgency. Medium = mất thời gian, High = mất tiền, Critical = mất cơ hội不可逆 |
| **Expected behavior vague** | Phải quote-able: "AI nói X" → "Expected: AI nói Y" |
| **Chỉ làm 1 lớp giải pháp** | Phải làm đủ 3: UI + Prompt + Architecture |
| **Demo chỉ là mô tả chung chung** | Demo phải cụ thể: system prompt đầy đủ, UI mockup rõ ràng, flowchart chi tiết |
| **Bỏ file trung gian** | Phải nộp cả 1-diverge.md và 2-converge.md (TA kiểm tra process) |
| **Không phản biện chéo** | Nếu có nhóm khác, trao đổi demo và nhận feedback |

---

## 🎯 LƯU Ý QUAN TRỌNG

1. **Bối cảnh nhất quán:** Mỗi lần dùng AI, đều phải đưa `00-context.md` vào đầu chat. Nếu không, AI sẽ sinh ra nội dung lạc đề.

2. **Không copy nguyên văn AI:** AI chỉ để brainstorm. Bạn phải đọc, chỉnh sửa, verify, và viết lại bằng ngôn ngữ của nhóm.

3. **Cross-file consistency:** 
   - Safety Question (Day 24) ↔ Test Set (Day 25) phải khớp
   - Primary failure (Day 24) ↔ 10-15 cases (Day 25) phải khớp
   - 3 giải pháp (Bài 2) phải giải quyết đúng rủi ro chọn

4. **Track-specific:** Tất cả nội dung phải xoay quanh Track 1 Admissions. KHÔNG copy worked example từ Track 3 Medical.

5. **Process matters:** TA sẽ kiểm tra bạn đã đi qua đủ 3 giai đoạn (Mở rộng → Hội tụ → Chốt) thông qua các file trung gian.

6. **Submission:** 
   - Tạo GitHub repo tên `Day25-MãNhóm` (ví dụ: `Day25-G001`)
   - Push toàn bộ thư mục `worksheet/` lên GitHub
   - README.md ở root điền thông tin nhóm
   - Nộp link qua LMS trước 23:59

---

## 📞 CẦN HỖ TRỢ THÊM?

Nếu nhóm bí:
1. **Đọc lại README.md** — hướng dẫn chi tiết nằm ngay trong file
2. **Đọc prompt tham khảo** — mỗi prompt có hướng dẫn cụ thể
3. **Xem worked example** trong `02-test-eval-plan.md` (Track 1 Admissions) — chỉ xem khi bí thật, đừng copy
4. **Hỏi instructor/TA** — nếu có Discord/Slack channel

**Chúc nhóm hoàn thành xuất sắc! 🚀**

---

*File này được tạo vào: 2026-05-13*  
*Dựa trên: Day 25 Lab Assignment PDF + track-bank-scenario-kit-v1.md + Day 24 completed files*
