# Readiness Score — Implementation Blueprint (Days 2–10)

**This is the single source of truth for the remainder of the capstone.** Each day below is written so that a *fresh* AI conversation, given only this document, can pick up building exactly where the previous day left off — no re-planning, no re-architecting, no re-deciding scope.

## Project summary (carry this into every daily conversation)

Readiness Score is a single self-contained HTML file (HTML/CSS/JS only, no external frameworks, no backend) that gives final-year CS/engineering students an honest 0–100 competitiveness score for internship applications, built from three modules: a Resume Scorer, a LinkedIn Scorer, and a fixed-length Mock Interview (4–5 questions on one project). The three sub-scores blend into one Readiness Score dashboard with a breakdown of what to fix first. Sessions persist in browser local storage. It calls the Claude API directly via `fetch`. It deploys as a static site on GitHub Pages.

**Locked v1.0 scope — do not add to this list on any day:**
- Resume Scorer, LinkedIn Scorer, Mock Interview (4–5 fixed questions), Unified Readiness Score, local storage history, GitHub Pages deployment.

**Explicitly excluded — do not build these even if it seems easy:**
- File/PDF upload or parsing (text paste only)
- Unbounded/deep multi-round interviews
- Accounts, login, backend, database
- Job-description-specific matching
- Native mobile app

---

## Day 2 — Design & Information Architecture

🎯 **Objective:** Turn the PRD into a concrete visual and structural design — no code yet, but every screen, state, and interaction should be decided by the end of today.

📖 **What I'll learn:** How to translate product requirements into a UI/UX design system and page flow before writing a single line of code, and why this step prevents redesign mid-build.

🛠 **Features to build:** None (design artifacts only — wireframes/spec, not working code).

📝 **Step-by-step implementation plan:**
1. Define the design system: color palette (dark theme, following the author's established premium-SaaS aesthetic — dark background, one accent color, IBM Plex Mono for data/scores, Inter for body, Space Grotesk or Sora for headings), spacing scale, and component styles (cards, buttons, score meters, input fields).
2. Sketch the single-page app structure: a top-level view switcher between Landing/Explainer → Resume module → LinkedIn module → Interview module → Dashboard/Report. Decide whether modules are tabs, a wizard/stepper, or a single scrolling page (recommendation: tabbed single-page app, since all data must stay in memory/localStorage together for the unified score).
3. Design the score visualization: how the 0–100 Readiness Score and the three sub-scores will be displayed (e.g., a large hero number + three horizontal meter bars, color-coded red/amber/green by range).
4. Design every state each module needs: empty state (before input), loading state (while Claude API call is in flight), result state (score + feedback shown), error state (API failure/rate limit).
5. Write out the exact copy for the persistent explainer banner and empty states in plain language (per the product's tone — direct, honest, non-generic).
6. Decide the local storage schema on paper: what keys, what shape of data, per session (this becomes the actual schema on Day 4, so get it right now).

📂 **Files and folders to create or modify:**
- `design-notes.md` — the design system, page flow, states, and localStorage schema decided today. This file is the reference for Day 3 onward.

🔗 **APIs, libraries, services, or tools to integrate:** None today.

🧪 **Testing tasks:** None (no code yet) — instead, sanity-check the flow by walking through it verbally: "a student opens the app, does X, sees Y, then Z" for all three modules plus the dashboard.

🐞 **Common issues and debugging tips:** The biggest risk today is under-specifying states (especially error and empty states) and having to redesign mid-build later. If unsure whether a state is needed, assume yes and write one line about it now.

✅ **End-of-day checklist:**
- [ ] Color palette, type scale, and component styles documented
- [ ] Full page flow (all modules + dashboard) sketched or described
- [ ] Every state (empty/loading/result/error) defined for each module
- [ ] localStorage schema written out
- [ ] Explainer/empty-state copy drafted

📸 **Expected project state and screenshots to capture:** No app yet — capture the `design-notes.md` file itself as today's artifact.

➡️ **Handoff notes for Day 3:** Day 3 will scaffold the actual HTML/CSS/JS file structure using exactly this design system and page flow — it should not need to make any new design decisions, only implement what's in `design-notes.md`.

---

## Day 3 — Project Setup & Static Shell

🎯 **Objective:** Create the single HTML file with full navigation between all views/modules working, styled per Day 2's design system, with no AI functionality yet (static/dummy content only).

📖 **What I'll learn:** How to structure a single-file HTML/CSS/JS app cleanly (view-switching pattern, CSS variable-based theming) so it stays maintainable as features are added.

🛠 **Features to build:** Navigation shell, persistent explainer banner (dismissible), all four view containers (Resume, LinkedIn, Interview, Dashboard) with placeholder/dummy content, dark theme styling.

📝 **Step-by-step implementation plan:**
1. Create `index.html` with the base HTML5 structure, a `<style>` block implementing the Day 2 color/type system as CSS custom properties, and a `<script>` block for JS logic.
2. Build the top-level shell: header/brand, navigation between the four views (Resume / LinkedIn / Interview / Dashboard), and a persistent dismissible explainer banner (state saved to localStorage so it stays dismissed).
3. Build each view container as a `<div class="view">` with a show/hide JS function (`showView(name)`), matching the Day 2 page flow exactly.
4. Add placeholder content in each view: a heading, a short description of the module, and a dummy input box or dummy result card — no real logic yet.
5. Build the empty state for the Dashboard view (since no scores exist yet, it should say so clearly, not show a broken 0/100).
6. Confirm responsive behavior at mobile width (~375px) and desktop width by resizing the browser.

📂 **Files and folders to create or modify:**
- `index.html` — the entire app lives here going forward. All future days edit this one file.

🔗 **APIs, libraries, services, or tools to integrate:** None today — no API calls yet.

🧪 **Testing tasks:**
- Click through all navigation — every view shows and hides correctly.
- Dismiss the explainer banner, refresh the page, confirm it stays dismissed (localStorage working).
- Resize browser to mobile width and confirm layout doesn't break.

🐞 **Common issues and debugging tips:**
- If views don't switch, check that `showView()` is removing an `active` class from all views before adding it to the target view, not just adding classes.
- If localStorage doesn't persist across refresh, confirm you're using `localStorage.setItem`/`getItem` with `JSON.stringify`/`JSON.parse`, not just assigning to a JS variable.

✅ **End-of-day checklist:**
- [ ] Single `index.html` file with all styling inline
- [ ] Navigation between all 4 views works
- [ ] Explainer banner dismissible and persists via localStorage
- [ ] Responsive at mobile and desktop widths
- [ ] Dashboard empty state renders correctly with zero scores

📸 **Expected project state and screenshots to capture:** Screenshot of the shell navigation working — each of the 4 views shown once, plus the dismissed/re-shown explainer banner.

➡️ **Handoff notes for Day 4:** The static shell and navigation are done. Day 4 wires up the local storage data layer (the actual schema from Day 2) so that module results can be saved and read back — still no Claude API calls yet, that starts Day 5.

---

## Day 4 — Data Layer (Local Storage)

🎯 **Objective:** Implement the full local storage data layer — saving, reading, and updating session data — using dummy/manually-entered scores, so the data plumbing is solid before real AI output flows through it.

📖 **What I'll learn:** How to design a small client-side data layer (load/save functions, a consistent schema) that the rest of the app treats as its single source of truth, rather than scattering `localStorage` calls throughout the UI code.

🛠 **Features to build:** `loadSession()` / `saveSession()` functions, a session history list, ability to see past sessions, manual "set a dummy score" buttons for testing (to be removed once real scoring exists).

📝 **Step-by-step implementation plan:**
1. Implement the localStorage schema from Day 2 as JS functions: `getState()`, `setState(partial)`, each reading/writing a single JSON object keyed e.g. `readiness_score_state_v1`.
2. Define the state shape concretely, e.g.: `{ resume: {text, score, feedback}, linkedin: {text, score, feedback}, interview: {projectText, qa: [], score}, history: [{date, overallScore}] }`.
3. Wire the Dashboard view to read this state and render the unified score (compute as a simple average or weighted average of the three sub-scores — weighting can be adjusted later, start with equal weights).
4. Add temporary "Set dummy score" buttons to each module (e.g., a button that sets `resume.score = 72` and re-renders) purely to test that data flows through to the Dashboard correctly. These are removed on Day 5 once real scoring replaces them.
5. Add a session history entry each time the Dashboard is viewed with a complete set of scores, capped at storing the last 20 sessions.
6. Build the History view/section (can be part of the Dashboard) listing past sessions with their overall score and date.

📂 **Files and folders to create or modify:**
- `index.html` — add the data-layer JS functions and wire the Dashboard/History views to them.

🔗 **APIs, libraries, services, or tools to integrate:** Browser `localStorage` API only.

🧪 **Testing tasks:**
- Set dummy scores in all three modules, confirm the Dashboard shows a correctly averaged unified score.
- Refresh the browser, confirm all data is still there.
- Clear one module's dummy score, confirm the Dashboard handles a partial state gracefully (doesn't show `NaN` or crash).
- Generate several dummy sessions, confirm History lists them in order with correct dates/scores.

🐞 **Common issues and debugging tips:**
- `NaN` in the unified score almost always means you're averaging over `undefined` — guard with a check like `scores.filter(s => typeof s === 'number')` before averaging.
- If history grows unbounded, confirm the array is sliced/capped on every save, not just checked once.

✅ **End-of-day checklist:**
- [ ] `getState()`/`setState()` functions implemented and used consistently
- [ ] Dashboard computes and displays a correct unified score from dummy data
- [ ] Partial/missing scores handled gracefully (no NaN, no crash)
- [ ] Session history saves and lists correctly, capped at 20 entries
- [ ] Data persists correctly across page refresh

📸 **Expected project state and screenshots to capture:** Dashboard showing a unified score computed from dummy sub-scores, plus the History view showing at least 2 saved sessions.

➡️ **Handoff notes for Day 5:** The data layer is complete and tested with dummy data. Day 5 replaces the dummy "set score" buttons in the Resume module with a real Claude API call that returns an actual score and feedback — this is the first day real AI functionality is added.

---

## Day 5 — Resume Scorer (First Claude API Integration)

🎯 **Objective:** Build the first real AI module: paste resume text in, get a real 0–100 score and specific feedback back from Claude, replacing the Day 4 dummy button for this module only.

📖 **What I'll learn:** How to call the Anthropic Messages API directly from a browser `fetch` call, structure a system prompt for consistent scoring output, and parse a plain-text (not JSON) response reliably.

🛠 **Features to build:** Resume text input, "Analyze my resume" button, loading state while the API call is in flight, rendered score + feedback result, error handling for failed calls.

📝 **Step-by-step implementation plan:**
1. Implement a shared `callClaude(messages, system)` helper function using `fetch("https://api.anthropic.com/v1/messages", ...)` with `model: "claude-sonnet-4-6"`, `max_tokens: 1000` — this same helper will be reused by the LinkedIn and Interview modules on Days 6–7, so build it generically now (accepts messages array + optional system prompt, returns the joined text content).
2. Write the Resume Scorer system prompt: instruct Claude to act as a skeptical, honest technical resume reviewer for early-career candidates, and to respond in a strict plain-text format (not JSON, to avoid parsing fragility) — e.g.:
   ```
   SCORE: <integer 0-100>
   STRENGTHS: <1-2 sentences>
   WEAKNESSES: <1-2 sentences>
   TOP_FIX: <the single most impactful change to make first>
   ```
3. Parse the response with simple line-based regex matching each label (`/^SCORE:\s*(\d+)/`, etc.) — do not attempt JSON parsing.
4. Wire the "Analyze my resume" button: on click, show the loading state, call `callClaude`, parse the result, call `setState` to save `resume.score`/`resume.feedback`, then render the result state.
5. Remove the Day 4 dummy "Set dummy score" button for the Resume module only (LinkedIn and Interview still use their dummy buttons until Days 6–7).
6. Handle the empty-input case: disable the "Analyze" button (or show an inline message) if the textarea is empty or under ~30 characters.
7. Handle API errors: wrap the call in try/catch; on failure show an error banner with a "Retry" button rather than a blank/broken state. For a 429 status specifically, retry once automatically after a short delay before showing the error.

📂 **Files and folders to create or modify:**
- `index.html` — add `callClaude()`, the Resume Scorer system prompt, response parsing, and UI wiring for the Resume module.

🔗 **APIs, libraries, services, or tools to integrate:** Anthropic Messages API (`https://api.anthropic.com/v1/messages`) via `fetch`, called directly from the HTML file per the artifact environment's handled authentication.

🧪 **Testing tasks:**
- Paste a real (or realistic sample) resume, confirm a sensible score and feedback render.
- Paste a very short/weak input, confirm the score and feedback plausibly reflect that (sanity-check Claude isn't giving 90+ to everything).
- Trigger the error state deliberately (e.g., temporarily break the fetch URL) and confirm the error banner + retry works, then restore the URL.
- Confirm the score reaches the Dashboard's unified score calculation correctly.

🐞 **Common issues and debugging tips:**
- If the response won't parse, log the raw `raw` text to the console first — Claude occasionally adds a stray preamble sentence even when instructed not to; tighten the system prompt with "Output ONLY the format below, no preamble" if this happens repeatedly.
- CORS errors calling the API directly usually mean this is being tested outside the artifact/environment context that handles authentication — confirm you're testing inside the intended environment.
- If scores feel too generous, add an explicit instruction like "Reserve scores above 85 for resumes with strong, specific, quantified achievements" to the system prompt.

✅ **End-of-day checklist:**
- [ ] `callClaude()` helper implemented generically for reuse
- [ ] Resume system prompt returns consistent, parseable plain-text output
- [ ] Loading, result, and error states all working for the Resume module
- [ ] Score correctly flows into the Dashboard's unified score
- [ ] Day 4's dummy button removed for this module

📸 **Expected project state and screenshots to capture:** The Resume module showing a real Claude-generated score and feedback after analyzing a sample resume; the error state triggered once for the record.

➡️ **Handoff notes for Day 6:** `callClaude()` exists and works. Day 6 repeats the same pattern for the LinkedIn module — same helper function, new system prompt tailored to LinkedIn profile text, same parse/render/error pattern. No new architecture needed.

---

## Day 6 — LinkedIn Scorer

🎯 **Objective:** Build the second AI module using the same pattern established on Day 5 — paste LinkedIn profile text, get a real score and feedback.

📖 **What I'll learn:** How to reuse an established integration pattern for a second, differently-scoped task — and how prompt design changes (not code structure) when the task changes.

🛠 **Features to build:** LinkedIn text input (About/Experience/Skills), "Analyze my profile" button, loading/result/error states, real Claude-scored output replacing the Day 4 dummy button for this module.

📝 **Step-by-step implementation plan:**
1. Write the LinkedIn Scorer system prompt, reusing the exact response format from Day 5 (`SCORE:`, `STRENGTHS:`, `WEAKNESSES:`, `TOP_FIX:`) for consistency — but tune the persona and criteria to LinkedIn specifics: is the headline searchable, does About avoid empty buzzwords, are all real experiences actually listed (a known real gap from the author's own profile audit — a completed internship missing from Experience entirely), are skills relevant and ordered well.
2. Reuse `callClaude()` unmodified — no changes to the shared helper.
3. Wire the LinkedIn module's input, button, loading/result/error states following the exact same JS pattern as the Resume module (copy the pattern, change the prompt and the `setState` key to `linkedin`).
4. Remove the Day 4 dummy button for the LinkedIn module.
5. Confirm the unified Dashboard score now correctly averages Resume + LinkedIn (Interview still pending/dummy until Day 7).

📂 **Files and folders to create or modify:**
- `index.html` — add the LinkedIn system prompt and wire the LinkedIn module's UI, following Day 5's pattern.

🔗 **APIs, libraries, services, or tools to integrate:** Same `callClaude()` / Anthropic Messages API as Day 5 — no new integrations.

🧪 **Testing tasks:**
- Paste a realistic LinkedIn profile text block, confirm sensible score/feedback.
- Deliberately paste a profile missing an obvious experience entry, confirm Claude's feedback catches something like this (validates the prompt is doing real analysis, not generic praise).
- Confirm error/retry behavior works identically to Day 5.
- Confirm Dashboard's unified score updates correctly with two real modules now.

🐞 **Common issues and debugging tips:**
- If LinkedIn feedback feels generic/interchangeable with resume feedback, the system prompt likely needs more LinkedIn-specific criteria (headline searchability, About section framing, experience completeness) rather than a copy of the resume rubric.
- Reminder: don't refactor `callClaude()` today even if tempted — keep changes isolated to the new prompt and UI wiring to avoid destabilizing the working Resume module.

✅ **End-of-day checklist:**
- [ ] LinkedIn system prompt returns consistent, differentiated feedback (not resume-feedback reworded)
- [ ] Loading/result/error states working for the LinkedIn module
- [ ] Score flows into Dashboard's unified calculation alongside Resume
- [ ] Day 4's dummy button removed for this module

📸 **Expected project state and screenshots to capture:** LinkedIn module showing real score/feedback; Dashboard now showing two real sub-scores blended.

➡️ **Handoff notes for Day 7:** Two of three modules are fully real. Day 7 builds the Mock Interview module, which is more complex — it's a multi-turn conversation (not a single call), so it needs its own state (question index, transcript) even though it still uses `callClaude()`.

---

## Day 7 — Mock Interview Module (Fixed-Length)

🎯 **Objective:** Build the Interview module: describe one project, answer a hard-capped 4–5 AI-generated follow-up questions, and receive a defensibility-based score — completing all three input modules.

📖 **What I'll learn:** How to manage a short multi-turn AI conversation client-side (conversation history array, turn counting) and enforce a hard stop condition so the feature can't accidentally become an unbounded chat.

🛠 **Features to build:** Project description input, question/answer chat-style UI, a hard-capped question counter (max 5), per-answer or end-of-session scoring, loading/result/error states.

📝 **Step-by-step implementation plan:**
1. Design the interview state: `interview.projectText`, `interview.turnCount`, `interview.transcript` (array of `{role, text}`), `interview.qaCount` capped at 5.
2. Write the interview system prompt: a skeptical technical interviewer persona, instructed to ask exactly one question at a time about the described project, each question building on the previous answer, in a strict format like:
   ```
   QUESTION: <one question>
   ```
3. On starting the interview: send the project description to Claude with the system prompt, render the first question.
4. On each answer submission: append to `transcript`, increment `turnCount`; if `turnCount >= 5`, stop asking new questions and move to scoring; otherwise call Claude again with the full transcript so far to get the next question.
5. Write the interview scoring system prompt (separate call, after the interview ends): send the full transcript, ask Claude to return `SCORE:` (0–100, based on specificity and defensibility of answers, not the project's inherent impressiveness) plus `STRENGTHS:`/`WEAKNESSES:`/`TOP_FIX:` in the same format used by Resume and LinkedIn, for UI consistency.
6. Wire the UI: a simple chat-style thread (question bubbles, answer input box below), a visible "Question X of 5" counter, and a result card once scoring completes.
7. Remove the Day 4 dummy button for the Interview module. Confirm the Dashboard now averages all three real sub-scores.

📂 **Files and folders to create or modify:**
- `index.html` — add interview state, the two interview system prompts (questioning + scoring), and the chat-style UI.

🔗 **APIs, libraries, services, or tools to integrate:** Same `callClaude()` — called multiple times in sequence within one interview session (once per question, once for final scoring).

🧪 **Testing tasks:**
- Run a full interview session end to end (5 questions), confirm it stops exactly at 5 and produces a final score.
- Give deliberately vague answers, confirm the score reflects that (should not score highly on vague answers).
- Give specific, detailed answers, confirm the score is meaningfully higher.
- Confirm the question counter and hard cap can't be bypassed (e.g., rapid double-clicking submit doesn't push past 5 questions).
- Confirm Dashboard now blends all three real modules correctly.

🐞 **Common issues and debugging tips:**
- If the interview asks more than 5 questions, the increment/check logic is likely happening after the API call fires rather than before — check the turn count before making the next "ask a question" call, not just before rendering.
- If questions feel repetitive rather than building on answers, confirm the full transcript (not just the latest answer) is being sent as context on each call.
- If scoring feels inconsistent with Resume/LinkedIn scoring style, reuse language directly from those prompts ("reserve high scores for...") for consistency.

✅ **End-of-day checklist:**
- [ ] Interview asks exactly one question at a time, capped at 5 total
- [ ] Full transcript used as context for each subsequent question
- [ ] Final scoring call produces SCORE/STRENGTHS/WEAKNESSES/TOP_FIX in the shared format
- [ ] Dashboard blends all three real sub-scores correctly
- [ ] Day 4's dummy button removed for this module

📸 **Expected project state and screenshots to capture:** A completed 5-question interview transcript with final score; Dashboard showing all three modules feeding a real unified Readiness Score.

➡️ **Handoff notes for Day 8:** All three modules are fully functional with real AI scoring. The app is feature-complete for v1.0. Day 8 is dedicated entirely to testing and polish — no new features — including cross-module edge cases and the visual/UX pass.

---

## Day 8 — Testing, Edge Cases & Polish

🎯 **Objective:** Systematically test the complete app, fix bugs, and polish the UI/UX — no new features today, only hardening what exists.

📖 **What I'll learn:** How to run a structured QA pass on a small web app (edge cases, error states, responsive check) and prioritize fixes by user impact before a deployment deadline.

🛠 **Features to build:** None new — bug fixes and polish only (loading spinners, transition animations, spacing/typography refinement, copy edits).

📝 **Step-by-step implementation plan:**
1. Run a full end-to-end pass as a first-time user: dismiss nothing, read every empty state and explainer, complete all three modules, view the Dashboard, refresh the browser, confirm history persisted.
2. Edge case pass: submit empty/whitespace-only input to each module (should be blocked with a clear inline message, not send a broken API call); submit extremely long input (~5000+ characters) and confirm it doesn't break layout or the API call; rapidly click submit buttons multiple times (should be disabled while a call is in flight, not fire duplicate requests).
3. Error simulation pass: temporarily break the API call (wrong URL) for each module one at a time, confirm every module shows a clear error banner with working retry, not a blank screen or console-only error.
4. Responsive pass: test at 375px (mobile), 768px (tablet), and 1200px+ (desktop) widths; fix any overflow, cramped spacing, or unreadable text at each size.
5. Visual polish pass: add a subtle loading spinner or animated dots during API calls (if not already present), smooth transitions between views, confirm consistent spacing/alignment across all four views, proofread all copy (explainer text, empty states, button labels) for clarity and tone.
6. Confirm the unified Readiness Score calculation is correct in all partial-completion states (e.g., only 1 or 2 of 3 modules done) — it should either show a partial score clearly labeled as partial, or prompt the user to complete the remaining module(s), never a misleading full score from incomplete data.
7. Write a short internal test log noting what was tested and what was fixed, to reference if regressions appear later.

📂 **Files and folders to create or modify:**
- `index.html` — bug fixes and polish only.
- `test-log.md` — brief record of what was tested and fixed today.

🔗 **APIs, libraries, services, or tools to integrate:** None new.

🧪 **Testing tasks:** (this entire day is testing — see implementation plan above for the full checklist)

🐞 **Common issues and debugging tips:**
- The most common late-stage bug is a race condition from double-submitted API calls — always disable the trigger button (`disabled = true`) the instant a call starts, and re-enable only in a `finally` block so it re-enables even after an error.
- If partial-completion Dashboard states look broken, that's usually the same `NaN`-from-averaging issue from Day 4 resurfacing in a new combination — recheck the guard clause.

✅ **End-of-day checklist:**
- [ ] Full end-to-end first-time-user pass completed with no broken states
- [ ] Empty/long/rapid-click edge cases all handled gracefully
- [ ] Error states verified for all three modules with working retry
- [ ] Responsive at mobile, tablet, and desktop widths
- [ ] Partial-completion Dashboard states are correct and clearly labeled
- [ ] `test-log.md` written

📸 **Expected project state and screenshots to capture:** Screenshots at all three responsive breakpoints; one screenshot of a caught-and-fixed bug (before/after if possible).

➡️ **Handoff notes for Day 9:** The app is fully tested and polished. Day 9 is deployment — getting this exact, tested `index.html` live on GitHub Pages, including resolving how the Claude API call will authenticate outside the artifact environment (this must be explicitly addressed, not assumed).

---

## Day 9 — Deployment to GitHub Pages

🎯 **Objective:** Get the tested v1.0 app live at a public GitHub Pages URL, with the Claude API integration working in the deployed (non-artifact) environment.

📖 **What I'll learn:** How static site deployment works via GitHub Pages, and how to responsibly handle an API call that needs authentication once outside an environment that handles it automatically.

🛠 **Features to build:** None new — deployment configuration only.

📝 **Step-by-step implementation plan:**
1. **Address the API authentication gap first, before deploying:** the artifact environment handles Claude API authentication automatically; a plain GitHub Pages site cannot securely hold a secret API key (anything in client-side JS is publicly visible). Decide and document one approach for this specific deployment — do not silently ship a hardcoded key. Two realistic options for a static-only v1.0: (a) keep the deployed version as a portfolio/demo build where the visitor briefly pastes their own API key into a prompt at runtime (stored only in memory, never persisted or transmitted anywhere else) with a clear on-screen explanation of why; or (b) present the deployed GitHub Pages site primarily as a live UI/UX demo with a clearly labeled "Try it with Claude" note directing to running it locally or in an environment with a configured key. Pick whichever fits how this will be presented (e.g., for a capstone demo, option (a) is usually simpler and still lets evaluators interact with it live). Document the choice at the top of the README.
2. Create a new GitHub repository (public) named e.g. `readiness-score`.
3. Manual step (guided): create the repo on github.com — click "New repository," name it, set to Public, do not initialize with a README yet since one will be added here.
4. Add `index.html` (final tested version from Day 8) to the repo root.
5. Write a `README.md`: project name, one-paragraph description, screenshot, the authentication approach decided in step 1, and a link to the live GitHub Pages URL (added after step 7).
6. Manual step (guided): push the repo — `git init`, `git add .`, `git commit -m "v1.0"`, `git remote add origin <repo-url>`, `git push -u origin main`.
7. Manual step (guided): enable GitHub Pages — in the repo, go to Settings → Pages → under "Build and deployment," set Source to "Deploy from a branch," select branch `main` and folder `/root`, click Save.
8. Wait a few minutes, then visit the generated `https://<username>.github.io/readiness-score/` URL and confirm the live site loads and functions identically to the local tested version, including the API key prompt from step 1 if that option was chosen.
9. Add the live URL to the README and to any existing portfolio/LinkedIn links.

📂 **Files and folders to create or modify:**
- New GitHub repository `readiness-score` containing `index.html` and `README.md`.

🔗 **APIs, libraries, services, or tools to integrate:** GitHub (repository + Pages hosting). No new code libraries.

🧪 **Testing tasks:**
- Load the live GitHub Pages URL on both desktop and a phone browser, confirm it works identically to the local version.
- Complete a full session (all 3 modules + Dashboard) on the live URL specifically, not just locally.
- Confirm the authentication approach chosen in step 1 works as intended and is clearly explained on-screen, not confusing to a first-time visitor.

🐞 **Common issues and debugging tips:**
- A blank page on the Pages URL almost always means the file isn't named `index.html` at the repo root, or Pages is still processing (wait 2–3 minutes and hard-refresh).
- If GitHub Pages shows a 404, double check Settings → Pages shows a green "Your site is live at..." confirmation, and that the branch/folder selected matches where `index.html` actually lives.
- If the live site's API calls fail with CORS or auth errors, this confirms step 1's authentication gap was real — do not skip it hoping it "just works" outside the artifact environment.

✅ **End-of-day checklist:**
- [ ] API authentication approach for deployment decided and documented before pushing
- [ ] Repository created and code pushed
- [ ] GitHub Pages enabled and live URL confirmed working
- [ ] Full session tested successfully on the live URL, desktop and mobile
- [ ] README complete with description, screenshot, and live link

📸 **Expected project state and screenshots to capture:** Screenshot of the live GitHub Pages URL in a browser address bar alongside the working app; screenshot of the Settings → Pages confirmation.

➡️ **Handoff notes for Day 10:** The product is live. Day 10 is presentation day — preparing to demo the live product and finalize/deliver the pitch deck, plus light final polish only if something is visibly broken on the live version.

---

## Day 10 — Final Polish, Demo Prep & Presentation

🎯 **Objective:** Ship the final, presentation-ready v1.0 — confirm the live product works flawlessly, rehearse the demo, and finalize the pitch deck for delivery.

📖 **What I'll learn:** How to prepare a technical product for a live demo (a rehearsed flow, a fallback plan if the live demo breaks) and how to present a scoped, honest v1.0 rather than apologizing for excluded features.

🛠 **Features to build:** None — this day is presentation and light final polish only, with a strict no-new-features rule to avoid last-day scope risk.

📝 **Step-by-step implementation plan:**
1. Do a final live-URL smoke test first thing: complete a full session on the deployed GitHub Pages site exactly as a demo audience would see it.
2. Fix only genuinely broken/visible issues found in step 1 — do not add anything not already in scope, even if a "quick win" idea comes up.
3. Prepare a demo script: a realistic sample resume snippet, LinkedIn snippet, and one project description ready to paste in during the live demo, so the demo isn't slowed down by typing or searching for content on the spot.
4. Rehearse the full demo flow once, timed: intro (30 sec) → Resume module (30 sec) → LinkedIn module (30 sec) → Interview module (60–90 sec, since it's multi-turn) → Dashboard reveal (30 sec) → close. Adjust the sample content if any module's output is confusing or slow to explain.
5. Prepare a fallback: take screenshots of a completed successful session (all 3 modules + Dashboard) in case of live demo failure (API rate limit, connectivity) during actual presentation — have these ready to show instead without breaking flow.
6. Review the Pitch Deck (delivered today alongside the PRD and this blueprint) against the finished product — confirm every claim in the deck (features, scope) matches what was actually built, and adjust deck language if anything shifted during the 9 days of building.
7. Write a short "what's next" note for v2.0 based on what was learned during the build (this becomes real backlog input, not just aspirational — e.g., "resume upload came up as the most-requested missing feature" if that pattern emerged).

📂 **Files and folders to create or modify:**
- `demo-script.md` — the rehearsed demo flow and sample content.
- Pitch deck reviewed/updated if needed (see Deliverable 3).

🔗 **APIs, libraries, services, or tools to integrate:** None new.

🧪 **Testing tasks:**
- Full rehearsal run-through of the demo script, timed.
- Final live-URL smoke test immediately before presenting (catches any overnight issues, e.g., API changes or Pages outages).

🐞 **Common issues and debugging tips:**
- If the live demo feels slow because Claude's response time varies, the loading state polish from Day 8 is what carries the demo through that gap — confirm it's reassuring, not alarming (e.g., "Reading your resume..." rather than a bare spinner).
- Resist any last-minute urge to "just quickly add" a feature — Day 10's only job is to make what exists work reliably and present well.

✅ **End-of-day checklist:**
- [ ] Live GitHub Pages URL smoke-tested and confirmed working
- [ ] Demo script written and rehearsed at least once, timed
- [ ] Fallback screenshots captured in case of live failure
- [ ] Pitch deck reviewed against the actual finished product
- [ ] v2.0 notes captured for future reference

📸 **Expected project state and screenshots to capture:** Full session screenshots (all 3 modules + Dashboard) from the live URL, used both as fallback material and as the final capstone artifact.

➡️ **Handoff notes:** Capstone complete. v1.0 is live, tested, and demo-ready. Any further work (resume upload, deeper interviews, job-matching) belongs to a v2.0 planning cycle, not a continuation of this 10-day scope.
