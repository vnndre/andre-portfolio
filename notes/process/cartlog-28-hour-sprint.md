# CartLog — 28.5-Hour Sprint

A constraint exercise in shipping over polishing. Goal: reimagine a receipt-scanning app from user research to working prototype inside a single sprint, with three design pivots forced along the way.

## The brief

"Rethink the receipt scanner." Most receipt-scanning apps are glorified OCR — take a picture, parse the text, add a row to a spreadsheet. Boring. The interesting question is *why people scan receipts at all* and whether the current apps are solving the right problem.

## Hour 0–6 — Research

Four short user interviews with people who either (a) actively use receipt-scanning apps or (b) have tried them and given up. Questions focused on the gap between the reason they downloaded the app and the reason they stopped using it.

**The recurring pattern:**
- People don't scan receipts to digitize receipts
- They scan receipts to answer a *future* question — "did I already buy this?", "how much have I spent on groceries this month?", "is that subscription still active?"
- The apps deliver the digitization but not the answer. You have to export the data into a spreadsheet or another tool to actually *use* it.

**The reframe:** Receipt-scanning isn't a data-entry problem. It's a context-retrieval problem.

## Hour 6–12 — Pivot 1: From ledger to recall

First design direction: a ledger app with a better UI. Clean list of receipts, fast categorization, summary views. Worked on wireframes for about 3 hours before realizing I'd just designed Mint with worse data.

Killed it.

## Hour 12–18 — Pivot 2: From recall to search

Second design: a search-first interface. Every receipt is indexed; you ask natural-language questions ("how much did I spend on coffee last month?") and get answers. Closer to the real problem. But:

- Requires a backend I can't build in a sprint
- Natural-language-to-SQL is the kind of thing where the demo sings and the real product stumbles
- The search experience only works if you have months of data. First-week users see an empty app.

Partial kill. Kept the "ask a question" framing but moved it off the critical path.

## Hour 18–24 — Pivot 3: Contextual surfacing

Final direction: the app doesn't wait for you to ask. It surfaces the context for you, at the moment you need it.

**Three core surfaces:**
1. **Scan** — camera-first, instant add. Same as every other app on this step, because this step has been solved.
2. **Budget view** — category rollups, month-to-date, week-over-week. A glanceable dashboard, not a spreadsheet.
3. **History** — a timeline view of your purchases organized by intent ("recurring", "one-time splurge", "reimbursable"), not by date.

The pivot: categorize by *why you bought it*, not *when you bought it*. The question "how much did I spend on discretionary stuff this month?" is the real question, and the app's job is to pre-answer it.

## Hour 24–28.5 — Ship

Working prototype in Figma with interactive flows. Three screens wired up end-to-end: scan → categorize → see impact on budget. A case study page written alongside the prototype that shows the pivots transparently — including the two directions I killed and why.

Uploaded to portfolio. Done.

## What the sprint taught me

**User research pays for itself inside the sprint.** The 6 hours of interviews at the front felt expensive. They saved me at least 12 hours of building the wrong thing (pivots 1 and 2 would have consumed that time if I hadn't caught them fast).

**Pivots are the deliverable when the constraint is time.** A clean final design is table stakes. The actual differentiator is showing that you got there by *trying and killing two other directions in public*, because that's what designers on real teams do. The case study leans hard into the pivot history for exactly this reason.

**Vibecoding is a force multiplier in the research phase.** I wasn't writing production code — I was sketching interfaces as fast as I could see them, and AI-assisted tooling lets you get a clickable prototype in the time it takes to draw one on paper. The 28.5-hour constraint is only reachable with modern tooling.

**Done > perfect, every time.** The final prototype has rough edges. Some transitions are janky. One flow doesn't have an empty state. It doesn't matter — the case study is about the decisions, and the decisions are clear.

## Artifacts

- Case study page: [andre-espinoza.com/cartlog](https://andre-espinoza.com/cartlog)
- Figma prototype link: *(TODO — drop here once assets/figma/ is populated)*
- Source repo: [github.com/vnndre/cartlog](https://github.com/vnndre) *(TODO — publish canonical React/Vite repo separately)*
