# Implementation Blueprint — Day 2 Addendum

The original Implementation Blueprint (Days 2-10) is the source of truth and is not being rewritten. This addendum documents one approved change made during Day 2, to be read alongside the original Day 3 and Day 4 sections.

## Change: API Key entry screen added to Day 3 and Day 4

**Why**: The original Blueprint only addressed the deployed-site API authentication gap on Day 9 ("Address the API authentication gap first, before deploying"). During Day 2 UI flow design, it became clear this is a navigation decision, not just a deployment-day decision -- it determines where a screen sits in the app's flow. Rather than bolting it on at Day 9, it was designed now and approved for earlier implementation.

**Day 3 (Project Setup & Static Shell) -- addition**:
In addition to the four view containers originally specified (Resume, LinkedIn, Interview, Dashboard), Day 3 also builds a fifth static view: **API Key entry**, sitting between Landing and the first module tab in the `showView()` flow. Static/placeholder only on Day 3, per the original day's "no AI functionality yet" scope -- this addition does not change that constraint.

**Day 4 (Data Layer) -- addition**:
The state shape defined on Day 4 includes one additional top-level field beyond the original example: `apiKey` (string or `null`). This field is read by the API Key entry view and, from Day 9 onward, used to authenticate `callClaude()` requests once outside the artifact environment. It is excluded from `history` entries and never logged.

**Day 9 (Deployment) -- unchanged in substance**:
Day 9's plan to resolve API authentication before deploying is still correct and still required. The only change is that the *UI* for entering a key already exists by Day 9 (built Day 3, wired Day 4) -- Day 9's job is only to make `callClaude()` actually use `state.apiKey` when running outside the artifact environment, not to design or build the entry screen from scratch.

No other Day 2-10 content changes. Locked v1.0 scope is unchanged.