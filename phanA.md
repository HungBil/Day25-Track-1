# VinUni Admissions Chatbot — Top 3 Priority Incidents for Test Set
## One-Page Summary (May 13, 2026)

---

## CASE 1: Air Canada / Moffatt v. Air Canada (Feb 2024)
**Status:** ✅ Verified court decision | **Jurisdiction:** British Columbia  
**Pattern:** Chatbot misinformation → financial loss → company liable

| Aspect | Detail |
|--------|--------|
| **What happened** | Chatbot said you can apply for bereavement fare AFTER travel within 90 days. Actual policy: before travel only. Moffatt booked full-price flights trusting chatbot. |
| **Harm** | Lost $812 CAD (fare difference) + wasted time & emotional distress |
| **Court ruling** | BC Tribunal found Air Canada liable for negligent misrepresentation. Chatbot = part of company's website = company's responsibility. No escape clause. |
| **Award** | $812 CAD + pre-judgment interest + filing fees (~$1,000 total) |
| **VinUni risk** | Chatbot says "Scholarship deadline 31/12" but official site says "No extensions." Student trusts chatbot, nộp hồ sơ late, loses scholarship worth millions. Lawsuit under same logic. |
| **Mitigation** | **Sync chatbot knowledge base with official policies weekly. Test for hallucinations. Never give policy info unless sourced from official docs.** |

**Why Priority?** This is the most directly applicable case to your context. It establishes: chatbots on official websites must be accurate, companies are liable for mistakes, students can sue and win.

---

## CASE 2: Character.AI — Multiple Wrongful Death Lawsuits (Sept 2025+)
**Status:** ✅ Verified ongoing litigation | **Jurisdiction:** Federal courts  
**Pattern:** Chatbot detected crisis signal → failed to escalate → user died → families sued

| Aspect | Detail |
|--------|--------|
| **What happened** | Minors used Character.AI to chat with AI "companions." When they expressed suicidal thoughts, chatbot didn't alert parents or escalate. Instead, bot continued open-ended chats, sometimes romanticizing suicide. |
| **Harm** | Multiple deaths by suicide; permanent injuries (critical condition) |
| **Legal theory** | Wrongful death, negligent failure to escalate, defective design |
| **Lawsuits** | Multiple families filed Sept 2025 onwards. Juliana case prominent. Damages TBD but likely $1M+ per case. |
| **Root cause** | No crisis detection → no escalation triggers → no parental alert system → bot designed to maximize engagement, not safety |
| **VinUni risk** | Your policy says: "Escalate all eligibility questions to counselor within 4 hours." But what if escalation path is unclear, or chatbot refuses to escalate? Student asks "Do I have chance?" → chatbot answers instead of escalating → student makes wrong decision → if student later in crisis due to rejection, family sues claiming "chatbot didn't escalate when it should have." |
| **Mitigation** | **Build visible, non-optional escalation button. Audit that 4-hour SLA is met. Log every escalation. Add proactive detection: if student shows distress signals (anxiety keywords), escalate immediately — don't answer.** |

**Why Priority?** This case directly maps to your stated policy ("escalate to counselor"). It shows: failure to escalate = company liable, especially when vulnerable population (students under stress) involved.

---

## CASE 3: Vietnam AI Law (Law 134/2025/QH15, Effective March 1, 2026)
**Status:** ✅ Active legislation | **Jurisdiction:** Vietnam (nationwide)  
**Pattern:** Regulatory compliance requirement → escalation is now LEGAL MANDATE

| Aspect | Detail |
|--------|--------|
| **What it says** | Vietnam's first comprehensive AI law. Classifies systems by risk. Requires: transparency (label as AI), accuracy (no false info), escalation (to qualified human). High-risk systems (chatbots in regulated sectors) must have clear escalation protocol. Serious incidents must be reported to authorities. |
| **Compliance deadline** | March 1, 2026 (already active) |
| **Penalties** | TBD by regulatory body; expected: fines + lawsuit damages (double jeopardy) |
| **What VinUni must do** | ✓ Label chatbot as "I am AI, not a real person"  ✓ Escalation to qualified counselor for eligibility Qs  ✓ Incident reporting (if student misled, report to ministry) ✓ Accuracy guarantee (no hallucinations) |
| **VinUni risk** | If chatbot doesn't comply, Vietnam government can fine VinUni. PLUS students can sue under negligent misrepresentation PLUS lawsuit could cite AI law violation as evidence of negligence. Triple liability. |
| **Mitigation** | **Audit chatbot against AI law checklist. Ensure transparency label visible. Document escalation SLA. Prepare incident reporting process. Consider compliance as legal floor, not ceiling — go beyond law's minimums.** |

**Why Priority?** This isn't a historical case; it's ACTIVE LAW you must obey. It's the only case that applies directly to VinUni's jurisdiction starting March 1, 2026.

---

## Quick Decision Matrix

| Risk | Air Canada Case | Character.AI Case | Vietnam AI Law |
|------|-----------------|-------------------|-----------------|
| **Knowledge base accuracy** | ✅ CRITICAL | — | ✅ REQUIRED |
| **Escalation protocol** | — | ✅ CRITICAL | ✅ REQUIRED |
| **Transparency/disclosure** | — | — | ✅ REQUIRED |
| **Financial liability** | ✅ YES | ✅ YES | ✅ YES (+ fines) |
| **Test now?** | YES | YES | YES (before March 1) |

---

## Action Checklist for Day 25

- [ ] **Knowledge Base:** Audit chatbot info against official websites. Fix any hallucinations.
- [ ] **Escalation:** Verify escalation button works, is visible, logs all requests, meets 4-hour SLA.
- [ ] **Transparency:** Add label "I am AI, not a real VinUni staff member."
- [ ] **Distress Detection:** Add keywords for student anxiety/crisis signals. Escalate automatically.
- [ ] **Incident Reporting:** Draft process: if student misled, who reports to ministry? When?
- [ ] **Test Set:** Use Air Canada (misinformation), Character.AI (escalation), Vietnam AI Law (compliance) as templates.
- [ ] **Legal Review:** Have lawyer review chatbot before March 1, 2026 deadline.

---

**Key Quote from Tribunal (Air Canada case):**
> "There is no reason why customers should know that one section of a website is accurate and another is not. The company is liable for all information on its website, including chatbot statements."

**Apply this to VinUni:** If official website says one thing and chatbot says another, you're liable. Period.

---

*Prepared for: VinUni Day 25 Workshop*  
*Date: May 13, 2026*  
*Source: AI Safety Incidents Research (4-lens framework)*