Day 48/60 — #ABTalksAIChallenge

Built: A Compare & Decide Engine for "Which Frontend Framework Should I Learn First?"

Every "React vs Vue vs Angular vs Svelte" article gives you someone else's opinion baked into a single verdict. I wanted to know what happens when I control the weights.

So I built a tool that doesn't answer the question — it lets you answer it, live, with real cited data.

What I Built:
✅ An interactive comparator scoring all 4 frameworks on Learning Curve, India Job Demand, Long-term Stability, and Performance
✅ Drag-and-adjust weight sliders — the ranking recalculates in real time based on what you actually care about
✅ A visible sources panel citing every data point (Stack Overflow Dev Survey, State of JS, npm trends, India-specific Naukri job data, bundle-size benchmarks)
✅ Every estimated (vs. directly sourced) number is explicitly flagged — no invented stats pretending to be facts
✅ A "How This Was Researched" panel that documents a real conflict I found in the data — React's bundle size was reported wildly differently across sources — and how I resolved it

Key Insight:
The hardest part wasn't the UI — it was refusing to fake precision. Two sources gave me completely different numbers for React's bundle size because they were measuring different things (bare library vs. real production stack). It would've been easy to just pick the more dramatic number. Instead I built the disagreement into the tool as a transparency feature. Trustworthy data tools should show their seams, not hide them.

What's Next:
Applying this same "weighted decision engine + cited sources" pattern to a career-decision tool next — because this shouldn't just work for tech stacks.

Building in public means admitting when the internet disagrees with itself — and showing your work instead of smoothing it over.

#BuildInPublic #AI #Claude #FrontendDevelopment #ReactJS #WebDevelopment #100DaysOfCode

@Anil Bajpai @ABTalks on AI @Anthropic