Learnings from Building NutriScope

A reflection on the design and engineering decisions behind NutriScope, a single-file HTML nutrition tracker.

1. Product & Domain Learnings


Nutrition targets need a formula chain, not a lookup table. Calorie needs depend on BMR (Mifflin–St Jeor equation) → activity multiplier → TDEE → macro split → fiber/micronutrient RDAs. Each layer depends on the one before it, so the code has to compute in that order every time a profile field changes.
Gender affects more than BMR. Iron and vitamin C RDAs differ by gender too, so "targets" can't be a single static object — they have to be recalculated from the whole profile.
Grams, not "servings," are the real unit of truth. Every food unit (1 roti, 1 cup, 1 glass) is really just a gram equivalence. Storing per-100g nutrition and converting via a unit-to-gram table made quantity/unit swapping trivial and kept the food database small and consistent.
Dietary preference is a filter, not a separate dataset. Tagging each food as veg / egg / nonveg and ranking those tags let one database serve all three preferences, instead of duplicating data three times.


2. Calculation Design


Percent-of-target is the universal currency. Once every nutrient is expressed as consumed / target, deficiencies, excesses, chart bars, and status pills all reuse the same number — no separate logic branches per nutrient.
Thresholds turn numbers into decisions. Picking <70% = deficiency and >130% = excess gives the recommendation engine clear triggers instead of vague "low/high" judgment calls.
Recommendations are just reversed lookups. Instead of hardcoding advice, the app sorts the existing food database by nutrient content and filters by diet — so "what should I eat more of" is answered by the same data structure used for logging, not a separate rules file.


3. UI/UX Decisions


One signature element earns the "premium" feel. Rather than spreading effort evenly, the energy ring (radial gauge with tick marks, like a lab instrument) became the one deliberate visual risk. Everything else — cards, tables, bars — stays quiet and consistent so the ring stands out.
Typography as a system, not a default. Pairing a display face (Space Grotesk) with a body face (Inter) and a monospace face (IBM Plex Mono) for all numeric data gives the app a "data instrument" identity rather than a generic dashboard look. Tabular/mono numerals also make columns of stats easier to scan.
Dark theme needs layered surfaces, not one flat background. Using --bg, --surface, --surface-2, and --surface-3 as a depth ladder (rather than one dark color everywhere) is what makes cards feel like they sit above the background instead of blending into it.
Color should encode meaning, not just decorate. Red/amber/green are reserved strictly for deficiency/excess/good status — no other UI element borrows those colors, so a glance at any bar or pill is immediately readable.


4. Engineering Approach


Single source of truth (state) with one render function. Every input (profile field, food log edit) mutates state and then calls renderAll(). This avoids partial UI updates getting out of sync and makes the data flow easy to reason about, even without a framework.
Derived data is never stored — only computed. Totals, targets, percentages, and recommendations are recalculated from state on every render rather than cached and updated piecemeal. This trades a small amount of performance for correctness and much simpler code.
Charts should re-use instances, not recreate them. Chart.js objects are created once and updated via .data mutation + .update() afterward, which avoids flicker and memory leaks from repeatedly destroying/rebuilding canvases.
No backend also means no persistence — and that's a real tradeoff. All state lives in memory and resets on page reload. For a demo/single-file tool this is an acceptable and expected limitation, but it's worth naming explicitly rather than leaving it implicit.


5. What I'd Do Differently Next Time


Add localStorage-based persistence (with a clear fallback message, since it's disabled in some sandboxed environments) so a day's log survives a refresh.
Support multiple meals/times of day rather than one flat daily log, to enable meal-timing insights.
Let users override default RDA assumptions (e.g., pregnancy, specific health conditions) since the current targets assume a generic healthy adult.
Cite real nutrition data sources (e.g., USDA FoodData Central) explicitly in-app, since the current values are reasonable approximations rather than verified lab data.