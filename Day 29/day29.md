Day 26/60 — Operation Lifeline: Supply Chain Crisis Lab
The Problem

Most supply chain content online is either a dry textbook diagram or a dashboard full of numbers with no story behind them. Beginners never get to feel what a crisis decision actually costs — they just read that "diversifying suppliers reduces risk" without ever trading off cost vs. speed vs. trust in real time. I wanted to build something where a complete beginner could walk into a fake company, get hit with a fake crisis, make real trade-off decisions, and walk out understanding why supply chain leadership is hard — not just that it is.

What I Built

A single-file React (CDN + Babel) simulation called Operation Lifeline: Supply Chain Crisis Lab — a full 7-stage crisis-management game:

🏭 Randomized company generator (industry, revenue, factories, suppliers, lead times, sourcing countries)
🔥 8 possible crisis events (factory fire, cyberattack, port strike, etc.), each with its own initial shock to 5 live metrics
🧭 A War Room where you pick 3 of 6 response actions, each with an honest "why this matters" trade-off, animated into live progress bars
🤝 A 4-round branching supplier negotiation tracking Trust, Price, and Lead Time
👔 A 5-question CEO Boardroom scoring executive decision-making
🤖 An AI Strategy stage — pick 2 of 5 real AI investments (Demand Forecasting, Supplier Risk Monitoring, etc.)
📊 A Final Dashboard computing 6 scored categories, biggest mistake, best decision, and personalized lessons learned — fully randomized every replay
The Design Decision That Mattered Most

The synergy system between crisis type and War Room actions. Instead of every action just being generically "good" or "bad," each of the 8 crises has 2 "ideal" actions that get amplified positive effects and dampened negative ones when chosen — while the other actions still work, just less efficiently. This meant I couldn't just tell the player which action was "correct." I had to write trade-off explanations that were true regardless of context, and let the fit between decision and situation be the thing that separates a good player from a great one. That's a much more honest teaching mechanism than a scored quiz with a right answer.

What I'd Improve Next

Right now the scoring formulas (Resilience, Cost Control, Risk Management) are hand-tuned weightings I judged to be "reasonable," not validated against any real supply-chain benchmark. Next iteration, I'd want to expose the scoring logic itself as a transparent panel — showing the player how their final score was calculated — so the simulation doubles as a lesson in supply chain KPIs, not just a black-box grade.

Tools Used

Claude (architecture, game balancing logic, and full single-file React build) · React 18 (CDN/UMD) · Babel Standalone (in-browser JSX) · Pure CSS (no Tailwind, no build step)

Key Insight

Quality of output is a direct function of quality of input context — and that held true for game design as much as prompting. The more precisely I specified why each trade-off existed before asking for the build, the less "generic edu-game" the final product felt.

60 days.  Learning supply chains and AI in public. #ABTalksAIChallenge @Anil Bajpai @ABTalks on AI @Anthropic