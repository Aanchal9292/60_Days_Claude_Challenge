# AI Supply Chain Control Tower — Learning Journal

## The Problem
Most "dashboard" demos are static — pretty charts, no consequences. I wanted to build something that actually simulates *pressure*: the feeling of being an Ops leader who has to make imperfect calls in real time, with KPIs that visibly react to every decision, good or bad.

## What I Built
A single-file, offline HTML/CSS/vanilla-JS game — **AI Supply Chain Control Tower**. The player is Head of Operations for 3 minutes. Alerts (port congestion, supplier delays, truck breakdowns, demand spikes, etc.) spawn on independent countdown timers, each with 4 possible actions that push 6 live KPIs (Service Level, Customer Satisfaction, Inventory Health, Transport Efficiency, Operating Cost, Revenue Protected) up or down. Ignoring or timing out an alert always costs more than acting — even imperfectly. Difficulty ramps: more alerts, shorter fuses, more overlap as the clock runs down. At the end, a weighted composite of KPI health, decision accuracy, and score produces a letter grade (A+ to D) with a written operational summary.

## The Design Decision That Mattered Most
Giving every alert **one clearly-best action out of four plausible ones**, rather than one obviously-correct action and three throwaway options. That's what makes the decisions feel real — "Approve Air Freight" isn't wrong for a port congestion alert, it's just not as sharp as it would be for a customs hold. The tension between plausible options is where the actual learning (and replay value) lives.

## What I'd Improve Next
- Persist high scores across sessions (currently resets on refresh — no localStorage was scoped in per single-file constraints)
- Add a difficulty-scaling "crisis chain" where ignoring one alert spawns a directly related follow-up alert, not just a KPI penalty
- Sound design (currently a visual-only toggle, per the brief)

## Tools Used
Claude (build), vanilla JS/CSS/HTML (single file, offline, no dependencies)

*Day [X] of #ABTalksAIChallenge — one build a day, shipped in public.*
