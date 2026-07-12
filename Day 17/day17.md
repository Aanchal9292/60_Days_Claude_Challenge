Day 17: The E85 Paradox — When Cheaper at the Pump Isn't Cheaper on the Road

The Problem

E85 flex-fuel gets marketed on one number: a lower price per liter than Petrol. But price per liter and cost per kilometer are not the same thing — mileage drag can quietly cancel out a pump discount. I wanted a dashboard that would settle this with actual data instead of forecourt marketing: does E85's ~18% cheaper price at the pump actually translate into cheaper driving, once you account for its weaker mileage?

What I Built

An interactive single-file HTML dashboard that ingests a 52-row fuel dataset (CNG, Diesel, Electric, Petrol E20, E85) and computes:

✅ Cost/km, CO₂/km, and Maintenance/km per fuel type, grouped and averaged from raw CSV columns
✅ Age-bucketed cost curves (New / Mid-life / Aged / Old) showing how running cost drifts as a car ages
✅ The "E85 Paradox" trio — pump saving (18%), running-cost penalty (+3.57%), and break-even price (₹79.11/L)
✅ A weighted 10-point E85 Suitability Score (cost 4pt, CO₂ 3pt, refuel 2pt, maintenance 1pt) with an animated SVG gauge
✅ Five fuel-comparison cards with pros/cons/best-for, with the user's own fuel (E85) glow-highlighted
✅ All charts — bar, doughnut, line, gauge — hand-built in raw SVG, no charting library, no CDN

The Design Decision That Mattered Most

Weighting the suitability score instead of just eyeballing the paradox numbers. It would've been easy to just show "18% cheaper, 3.57% more expensive to run" and let the reader do the math. But a single weighted score (cost-heaviest, since that's what actually hits a wallet monthly) turns three disconnected percentages into one honest verdict: 5.71/10 — E85 wins decisively on emissions, loses decisively on cost, and the score reflects that trade-off instead of hiding it behind good pump-price optics.

What I'd Improve Next


Pull in a larger, multi-city dataset to check if the break-even price holds outside this sample, since 11 rows per fuel is a thin base for a break-even claim
Add a real amortized maintenance curve (currently averaged flat per age bucket, not fitted) so the age-vs-cost line reflects actual depreciation-of-reliability patterns
Let the user override "their" fuel/vehicle/km inputs directly in the dashboard UI instead of baking in dataset-derived defaults, so it works as a genuine personal calculator, not just a dataset visualizer


Tools Used

Claude API · Single-file HTML/CSS/JS · Pure SVG (no chart library, no CDN) · CSV data analysis (Python/pandas-style grouping) · Dark glassmorphism design system


#ABTalksAIChallenge — Day 17 of 60. One build a day, no exceptions.