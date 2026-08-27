# Project Structure — Readiness Score

Deliberately minimal, matching the locked "single HTML file, no build step, no framework" architecture. Adding `/src`, `/components`, `/assets`, or `/tests` folders would contradict this architecture, so none are created.

```
readiness-score/
├── index.html          # The entire app. All application code lives here.
├── design-notes.md     # Day 2 design system, page flow, states, and localStorage schema.
├── ARCHITECTURE.md      # System architecture.
├── SCHEMA.md            # localStorage schema.
├── API.md               # Claude API call contracts.
├── UI-WIREFRAMES.md     # User flow and wireframes.
├── PROJECT-STRUCTURE.md # This file.
├── BLUEPRINT-ADDENDUM.md # Day 2 approved change: API key screen added to Day 3/4.
├── test-log.md          # Day 8 QA review findings and fixes.
├── LICENSE              # MIT License.
└── README.md            # Project description, live link, setup instructions, cost/security disclosures.
```

## What lives where

- **`index.html`** is the only file containing application code. Internally it is organized top-to-bottom as:
  1. `<style>` block -- CSS custom properties for the design system (colors, type scale, spacing), plus component styles (cards, buttons, meter bars, inputs).
  2. View containers -- one `<div class="view">` per screen (Landing, API Key, Resume, LinkedIn, Interview, Dashboard), shown/hidden via a `showView(name)` function.
  3. `<script>` block -- in dependency order: state layer (`getState`/`setState`) → shared `callClaude()` helper → per-module logic (parsing, wiring) → view-switching logic.
- **`design-notes.md`** is the Day 2 working reference that the four polished deliverable docs above are derived from -- kept as the single source Day 3 reads from when scaffolding the static shell.
- **Root-level `.md` files** are documentation and planning artifacts only; none are ever loaded or referenced by `index.html` at runtime.

## Why this structure

The project's entire value proposition (per the Blueprint) is a single-file, zero-install, zero-build app that a fresh AI session or a new developer can pick up with full context by reading one HTML file plus these docs. Any folder nesting or build tooling would work against that goal without adding real capability at this scope (three scoring modules, no accounts, no backend). This also means Day 3 onward never needs directory-structure decisions -- there is exactly one place new code goes.