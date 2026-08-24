Day 58/60 — #ABTalksAIChallenge

Today's job was to break my own app on purpose, before someone else did it for me.

I put on a QA reviewer's hat and went through everything with the assumption this launches publicly tomorrow — bugs, edge cases, security gaps, accessibility, performance, the works. Not "does it work when I use it correctly," but "what happens when someone doesn't."

What I Built (so far, not yet tested or deployed):
✅ Offline detection — a dropped connection now shows a clear message instead of a confusing generic error
✅ Raised the interview answer minimum so "ok" and "yes" can't pass as real answers
✅ A second layer of duplicate-submission protection, beyond just disabling a button
✅ A soft warning for excessively long input, without blocking the user
✅ Named the one real unresolved risk out loud instead of hiding it: the API key lives in plaintext in the browser's local storage, because there's no backend to hold it more safely. That's a deliberate tradeoff of this architecture, not an oversight — but it deserves to be said plainly, not buried.

Key Insight:
A QA pass isn't "does the demo work when I click the happy path." It's "what's the dumbest, fastest, most broken way someone could interact with this — and does it fail gracefully instead of just failing." Most of today's fixes exist because of that second question, not the first.

What's Next:
Actually verifying these fixes work — offline mode, short answers, long pastes — then finally deploying live. Code that's been reviewed carefully isn't the same as code that's been run.

A security tradeoff you've named honestly is safer than one you've buried. Today's post says which one this is.

#ABTalksAIChallenge #BuildInPublic #AI #Claude @Anil Bajpai @ABTalks on AI @Anthropic