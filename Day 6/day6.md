# Day 6: Building an ATS Resume Optimizer with Claude
### #ABTalksAIChallenge | 60-Day Claude AI Mastery Challenge

---

## 🎯 What I Built Today

An **ATS Resume Optimization system** — a structured prompt that turns Claude into a resume rewriting expert. I fed it my real resume (as an uploaded file) and asked it to:
1. Score the original resume for ATS-friendliness
2. Rewrite it for both machine parsing AND human recruiter readability
3. Output a polished, one-page, PDF-ready resume

Instead of asking "make my resume better" (vague, low-quality output), I engineered a prompt with strict **roles, rules, and output structure**.

---

## 🧠 The Prompt Anatomy I Used

| Element | What I Specified |
|---|---|
| **Role** | "You are an ATS optimization expert and resume writer" |
| **Task** | Score + rewrite resume, keep every claim truthful |
| **Constraints** | Never invent achievements/metrics; use only source info |
| **Format** | Exactly 2 parts — ATS Score, then Final Resume |
| **Structure** | Fixed section order (Summary → Education → Experience → Projects → Skills → Certifications) |
| **Output spec** | Single column, no tables/icons/images, one-page A4, PDF-ready |

This is **Prompt Engineering Law #1** in action again: *the quality of the output is a direct function of the quality of the input context.* The more precisely I defined the rules, the less room Claude had to improvise — or hallucinate.

---

## 🔑 Key Learnings

**1. Anti-hallucination constraints actually work.**
By explicitly instructing "never invent achievements, skills, or metrics — if info is missing, suggest improvements instead," Claude flagged real gaps in my resume (no Experience section, no quantified project outcomes) instead of making something up to fill the space. That's a trustworthy AI tool, not just a fluent one.

**2. Format specificity prevents rework.**
Telling Claude exactly what NOT to use (no tables, no columns, no icons) upfront saved a full revision cycle. ATS systems choke on visual formatting — most people don't know their "beautiful" resume template is often unreadable to the software screening it.

**3. A rigid output contract makes results reusable.**
By locking Claude into "exactly two parts, nothing else," I got a clean, predictable output every time — no wandering intros, no extra commentary. This is the same principle as structured JSON prompting: constrain the shape of the answer, not just the content.

**4. Honesty about gaps is more valuable than fake polish.**
The most useful part of the output wasn't the rewritten resume — it was Claude pointing out *what was missing* (no internship/work experience, no measurable project outcomes) so I know exactly what to build next.

---

## 💡 Quotable Insight

> "A good resume prompt doesn't just ask AI to write better — it tells AI exactly what 'better' is allowed to look like."

---

## 🔗 Deliverables

- ✅ ATS-optimized, one-page, PDF-ready resume (single column, ATS-parsable)
- ✅ ATS Score comparison (Before: 58/100 → After: 92/100)
- ✅ This learning journal
- ⏭️ Next: Turn this into a reusable "Resume Optimizer" interactive artifact (upload resume → get scored + rewritten version)

---

*Day 6 of 60 | #PromptEngineering #ATSOptimization #AIforCareers #ClaudeAI #LearningInPublic*
*Tagging: @Anil Bajpai @ABTalks on AI @Anthropic*
