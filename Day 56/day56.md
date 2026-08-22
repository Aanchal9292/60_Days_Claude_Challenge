Day 56/60 — #ABTalksAIChallenge

Today was supposed to be a simple "wrap up the MVP" day. It turned into a lesson about scope honesty instead.

The plan handed to me said: finish everything, deploy live, all in one sitting. But my actual 10-day blueprint had this work spread across four separate days — LinkedIn scoring, mock interviews, dedicated testing, and deployment, each with its own day for a reason. Compressing all of that into a few hours isn't "efficient," it's just rushed.

I chose to compress it anyway — but going in with eyes open about the tradeoff, not pretending it's risk-free.

What I Built (so far, not yet tested or deployed):
✅ LinkedIn Scorer — real Claude integration, catches missing experience entries and generic headlines instead of giving empty praise
✅ Mock Interview module — multi-turn Q&A, hard-capped at exactly 5 questions, scores based on how well you defend your answers, not how impressive the project sounds
✅ Footer requirement added and verified across every view
✅ All three scoring modules now share one clean, reused API-calling pattern

Key Insight:
A hard cap that's checked before firing the next request, not after, is the difference between "exactly 5 questions" and "somehow 6 questions." Small ordering details like that are where AI-assisted builds quietly break if you don't slow down to check the logic.

What's Next:
Actually testing this locally, then deploying to GitHub Pages and confirming the live version works end to end — the part that turns "code that exists" into "a demo I can show someone."

Built fast today. Verified next. Those aren't the same milestone, and I'm not going to post them like they are.

#ABTalksAIChallenge #BuildInPublic #AI #Claude @Anil Bajpai @ABTalks on AI @Anthropic