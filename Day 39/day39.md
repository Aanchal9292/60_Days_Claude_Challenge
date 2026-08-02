Day 39/60 of #ABTalksAIChallenge: I built a PDF Splitter & Merger that never uploads your files anywhere

Every "free" online PDF tool works the same way: you upload your document to someone else's server, wait, then download the result. For contracts, resumes, or anything remotely sensitive, that's a quiet privacy trade-off most people never think about.

So today I built a tool that skips the server entirely.

What I Built:
✅ A single-file HTML app — PDF Splitter & Merger — that runs 100% client-side
✅ Splitter with 4 modes: custom ranges, split-after-page, every-N-pages, and click-to-select page extraction
✅ Live page thumbnails with a preview modal, drag-to-reorder merge queue, and real-time validation on every input
✅ A "resulting document structure" preview that shows exactly what files will be generated before you commit
✅ Full dark mode, keyboard shortcuts, drag-and-drop, and offline support after first load
✅ Zero uploads — every page render, split, and merge happens in your browser using pdf-lib and pdf.js

Key Insight:
The hardest part wasn't the PDF manipulation — libraries handle that. It was designing trust into the UI. When there's no server round-trip, you have to show the user their file never left the tab: instant thumbnails, immediate validation, no spinner waiting on a network call. The absence of a loading screen became the actual proof of privacy.

What's Next:
Exploring how far client-side document processing can go before the browser becomes the bottleneck — next up, something with heavier file manipulation.

Sixty days in, the pattern keeps repeating: the most "boring" utility problems often hide the most interesting constraints.

#ABTalksAIChallenge #BuildInPublic #Claude #AI #WebDevelopment #FrontendDevelopment

@Anil Bajpai @ABTalks on AI @Anthropic