Day 16/60 — AI-Powered Stock Fundamental Research Tool

#ABTalksAIChallenge

The problem

Most "AI stock analysis" tools I'd seen fall into one of two traps: either they hedge so hard they say nothing useful, or they slide into giving actual buy/sell calls dressed up as "analysis" — which is a step past what an AI (or honestly, most content online) should be doing for someone's real money. I wanted to build something that draws a hard line: full evidence-based fundamentals, zero recommendations.

What I built

A single-file, Claude API-powered stock research tool covering Indian and global listed companies, with five distinct analysis modes:


Quick Take — a 150-220 word snapshot: valuation verdict, D/E, ROE, ROCE, growth trend, 3 strengths, 2 watch-points, overall fundamental quality
Deep Dive — a full structured report across 8 sections (Snapshot, Valuation, Growth, Health, Returns, Peers, Ownership, View), each using tables for the underlying data
Compare — side-by-side metrics for two stocks, "where each one leads," no declared winner
Pros & Cons — 3-5 evidence-backed strengths and risks, each tied to a specific figure
Portfolio Fit — takes a person's existing holdings and analyzes concentration/overlap for a new stock, without advising for or against adding it


Every mode runs on the same mandatory rule set: cite a source next to every key figure, flag missing data instead of inventing it, and never issue a buy/sell/hold call or target price.

The design decision that mattered most

Enabling live web search in the API call, not just relying on the model's training data. Stock fundamentals — CMP, P/E, promoter holding, quarterly EPS — are only useful if they're current. A model answering purely from memory would silently give you last year's numbers with this year's confidence. So the tool calls Claude with the web_search tool turned on, and the system prompt enforces a source priority (Screener → Tickertape → Moneycontrol → NSE → BSE → filings) with a hard instruction to flag anything it can't verify rather than fabricate it.

This is the same anti-hallucination discipline from my resume and environmental-dashboard work, just applied to a domain where the stakes of a wrong number are financial rather than personal — which made me hold the line even more strictly here.

What I had to leave out

The original spec referenced a custom HTML template for the Deep Dive mode with actual tabbed navigation (Snapshot / Valuation / Growth / etc. as clickable tabs). I didn't have that template file, so Deep Dive currently renders as scrollable markdown sections with the same headings instead of true tabs. Functionally equivalent, visually simpler — a good reminder that "prepare project for X" sometimes means building the 90% you can verify and being explicit about the 10% you couldn't.

My honest takeaway

Building this made the line between "informative" and "advice-giving" much clearer to me than reading about it would have. It's genuinely easy for a report to slide into implicit advice — a confident valuation verdict, a strongly worded "strength," a growth trend stated as a forecast rather than a fact — without ever using the words "buy" or "sell." Writing the system prompt forced me to separate three things explicitly: what's a fact (a cited number), what's an interpretation (this D/E is "moderate"), and what's a probability (a trend might continue). That three-way split is now a pattern I want to reuse anywhere I'm building something that touches someone's money or life decisions — not just this tool.

Tools used


Claude Sonnet (direct API call with the web_search tool enabled)
marked.js for markdown-to-HTML rendering
Single-file HTML/CSS/JS, no build step



Part of the 60-day AI mastery challenge — build daily, document honestly, share publicly.