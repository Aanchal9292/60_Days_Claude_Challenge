Day [X]/60 — AI Red Flag Detector for Job Postings

#ABTalksAIChallenge

The problem

I was about to spend an hour customizing a resume and cover letter for a job posting before I'd actually checked whether the posting itself was worth the time. Vague responsibilities, no salary, no location — these are all things I notice eventually, but only after reading closely. I wanted something that catches them in one pass, before I invest effort.

What I built

An AI Red Flag Detector — a prompt-based system that takes a job description and company info as input and returns a structured risk report:


Unrealistic requirements — excessive experience asks for the level, too many responsibilities crammed in, contradictory expectations
Toxic workplace signals — burnout indicators, "wear many hats," hustle-culture language ("rockstar," "fast-paced"), poor work-life balance cues
Remote job authenticity — hidden office requirements, relocation expectations, misleading remote claims
Hiring risks — missing salary/stipend info, vague responsibilities, suspicious hiring practices
Company risks — reputation, stability, growth vs. layoff signals


The output is a full report: overall risk score (0–100), top red flags with severity ratings, positive signals, a risk breakdown table by category, a final verdict (Apply / Apply with Caution / Avoid), and — the most useful part — five interview questions generated specifically to validate whatever risks it found.

Test case

I ran it against a live posting: Front End Developer Intern at ArGo Intern (Argo Inter E-Learning Providers).

Result: 58/100 — Apply with Caution

CategoryRiskRequirementsLowCultureLowRemote authenticityUnstatedHiring practicesMedium–highCompany stabilityMedium

What stood out: this posting had none of the classic toxic-culture red flags. Responsibilities were realistic for intern level, the tech stack (HTML/CSS/JS/React) was specific and consistent, no hustle-culture language anywhere. But it scored moderate risk anyway — because stipend, work location, and internship duration were never mentioned at all.

The insight

Most red-flag detection I'd seen (and initially designed for) focuses on bad language present — hustle-culture buzzwords, contradictory asks, excessive requirements. But a huge share of real risk lives in information that's simply absent. A posting doesn't need a red flag phrase to be risky; it just needs to leave out the three things you'd need to make an informed decision.

This changes how the tool needs to score things: it can't just pattern-match on toxic phrases, it has to treat silence on key fields (comp, location, duration, growth path) as its own risk signal.

Where this goes next


Add a layer that cross-references the posting against my own resume — not just "is this posting risky" but "is this posting risky for me specifically"
Build a lightweight version I can run against every shortlisted posting before applying, not after
Track outcomes over time — did "apply with caution" postings actually turn into more ghosting/vague offers than "apply" ones?


Tools used


Claude (Sonnet) for the detector logic and report generation
Structured prompt with defined categories, severity scoring, and output schema
HTML/CSS single-file report design for a shareable, dossier-style output



Part of the 60-day AI mastery challenge — build daily, document honestly, share publicly.