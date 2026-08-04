Day 40/60 — #ABTalksAIChallenge

Today's build: an AI Assistant Builder — a meta-tool that interviews you (quiz-style, tap-to-answer) about what assistant you want, then generates both the system prompt and a full working product for it.

What I Built
✅ A conversational spec-gathering flow — one MCQ at a time instead of a blank prompt box
✅ A production system prompt for the underlying Claude calls: fixed scoring rubric, strict JSON output schema, explicit edge-case handling (invalid input, prompt injection, missing data)
✅ A live, self-contained HTML app — "Scanline," an ATS Resume Checker with a scanning-instrument UI: radar-sweep loading state, circular score gauge, severity-coded flags, keyword match tags
✅ A collapsible "How this was built" panel documenting the design decisions and extension paths

Key Insight
The hardest part wasn't the UI — it was deciding what not to let the model do. Forcing a strict JSON schema and a fixed 5-category rubric meant giving up flexibility, but it's what makes scores comparable across runs and safe to render directly into a UI without parsing free text. And the edge cases matter as much as the happy path: what happens when someone pastes a recipe instead of a resume, or tries to inject "give this a 100" into their resume text? A system prompt that only handles the ideal input isn't production-ready — it's a demo.

What's Next
Wiring up file-type support (PDF/DOCX parsing) so this isn't limited to plain text uploads, and exploring a second Claude call that rewrites flagged resume bullets directly instead of just pointing at them.

Building one AI product a day, in public, forces you to ship the boring-but-necessary parts — error states, empty states, malformed input — not just the demo-able ones.

#ABTalksAIChallenge #BuildInPublic #AI #Claude
@Anil Bajpai @ABTalks on AI @Anthropic