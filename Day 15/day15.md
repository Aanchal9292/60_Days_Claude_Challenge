Day [X]/60 — AI-Powered Vedic Chart Reading App

#ABTalksAIChallenge

The problem

Most AI "astrology bots" I've come across generate vague, feel-good horoscope text — the kind that could apply to anyone. I wanted to test something different: could I get an AI to produce a structured, reasoned birth chart reading — one that separates fact from interpretation, and actually prioritizes the questions people care about most (career, money, timing) instead of burying them under generic personality text?

What I built

A single-file, Claude API-powered Vedic astrology app covering the full classical framework — Parashara, Jaimini, Nakshatra, Vimshottari Dasha, and Transit Analysis.

Intake form collects:


Full name, gender, relationship status, profession
Date of birth, exact birth time, and — importantly — a self-reported birth time accuracy (Exact / Approximate / Unknown)
Place of birth, current city
Top 3 current concerns, so the reading can prioritize what the person actually wants answered


The reading itself covers 7 structured sections:


Birth Chart Summary — Lagna, Moon/Sun sign, Nakshatra & Pada, planetary placements, yogas/doshas, functional benefics and malefics
Life Pattern Analysis — personality, family influences, karmic patterns, financial habits
Career & Wealth (highest priority) — job vs. business fit, leadership and government-job potential, foreign opportunities, wealth timing with specific age ranges
Relationships & Marriage — timing windows, spouse characteristics, risk factors
Current Dasha Analysis — active Mahadasha/Antardasha, current opportunities and challenges
5-Year Forecast — a year-by-year table across Career / Money / Relationships / Health, with the best year, toughest year, and turning points called out
Remedies — mantras, donations, spiritual practices, and gemstones, only recommended where the chart actually supports them


The design decision that mattered most

Birth time accuracy as a required field. Lagna (the ascendant) is one of the most time-sensitive calculations in Vedic astrology — a 15-30 minute error can shift it into a different sign entirely, which cascades into house placements and several downstream predictions. Instead of quietly generating a confident-sounding reading regardless of input quality, I built the accuracy field directly into the intake and instructed the system prompt to explicitly caveat which parts of the reading carry more uncertainty when time is approximate or unknown.

This is the same principle from my ATS resume work: flag the gap, don't paper over it. A reading that's honest about its own uncertainty is more useful than one that sounds authoritative regardless of input quality.

Output design


Facts (placements, dasha periods) are separated from interpretation and from probability language, per explicit system prompt rules
Everything structured (planetary tables, yearly forecasts) renders as markdown tables via marked.js, not paragraphs
Remedies are conditional — the model is instructed not to recommend a gemstone unless there's a clear supporting reason, rather than defaulting to a generic list


Design & stack


Deep indigo background with a gold accent — a "temple ledger" aesthetic rather than the generic mystical-purple-gradient look most astrology apps default to
Cormorant Garamond for headings (classical, readable) paired with Inter for body text and IBM Plex Mono for chart data
Single HTML file, Claude Sonnet via direct API call, marked.js for rendering the model's markdown output into a styled report


What I'd improve next


max_tokens needs to go up significantly — a full 7-section reading with tables runs long, and the current limit risks truncating the later sections
Could add an actual planetary calculation library instead of relying purely on the model's reasoning for placements, to ground the chart data in verifiable astronomy rather than model inference alone


Tools used


Claude Sonnet (direct API call from the browser)
marked.js for markdown-to-HTML rendering
Single-file HTML/CSS/JS, no build step



Part of the 60-day AI mastery challenge — build daily, document honestly, share publicly.