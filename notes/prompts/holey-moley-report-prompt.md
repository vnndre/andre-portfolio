# Holey Moley Review Report Prompt

The Claude prompt that powers the weekly review report in [weekly-review-bot](https://github.com/vnndre/weekly-review-bot). Lives inside the "Process CSV & Build Prompt" Code node — the node pre-computes every metric, then hands Claude the numbers + raw reviews + a strict format instruction.

## Design philosophy

**The model never does math.** Every number in the final report is calculated by deterministic JavaScript before the prompt is assembled. Claude's job is strictly narrative: theme detection, quote selection, trend commentary, focus points. If a number is wrong, it's a bug in the Code node — not a model hallucination.

**The model gets the exact format.** The prompt ends with an explicit Markdown structure. No "write a report in whatever format makes sense". The format is the contract.

**The model gets the real raw text.** Review content is passed through verbatim — no summarization, no filtering. If the guest wrote "the lighting in the bathroom gave me a migraine", Claude sees that exact sentence and can quote it.

## Prompt template (as assembled at runtime)

```
You are generating a weekly customer feedback report for {{VENUE_NAME}} ({{VENUE_DESCRIPTION}}).

REPORT PERIOD: Week {{weekNum}} ({{periodLabel}}) — {{weekStartDisplay}} – {{weekEndDisplay}}
FISCAL INFO: {{fyLabel}}

COMPUTED METRICS (use these exact numbers):
- Total Reviews (active, non-deleted): {{totalReviews}}
- Weekly Average Rating: {{weeklyAvg}}
- PTD Average ({{periodLabel}}): {{ptdAvg}} ({{ptdCount}} reviews)
- YTD Average ({{fyLabel}}): {{ytdAvg}} ({{ytdCount}} reviews)
- Deleted this week: {{deletedThisWeek}}
- Deleted {{periodLabel}} to date: {{deletedPTD}}
- Deleted {{fyLabel}} to date: {{deletedYTD}}
- Response Rate: 100%
- Response Time: < 1 day

RATING DISTRIBUTION (non-deleted):
5★ – {{count}} ({{pct}}%)
4★ – {{count}} ({{pct}}%)
3★ – {{count}} ({{pct}}%)
2★ – {{count}} ({{pct}}%)
1★ – {{count}} ({{pct}}%)

SOURCES (non-deleted):
Google – {{count}}
Yelp – {{count}}
TripAdvisor – {{count}}

DELETED REVIEWS ({{deletedThisWeek}} total, excluded from all ratings):
- {{authorInitials}} ({{rating}}★ {{source}}): {{reviewText}}

PROMOTER REVIEWS (4-5★):
- {{authorInitials}} ({{rating}}★ {{source}}, {{date}}): {{reviewText}}

NEUTRAL REVIEWS (3★):
- {{authorInitials}} ({{rating}}★ {{source}}, {{date}}): {{reviewText}}

DETRACTOR REVIEWS (1-2★):
- {{authorInitials}} ({{rating}}★ {{source}}, {{date}}): {{reviewText}}

NAME MENTIONS (auto-detected from reviews — reviewer should verify these are actual staff):
{{name}}: {{count}}

COMPARISONS FROM HISTORY:
- Prior Week: {{count}} reviews at {{rating}}★ (change: ↑/↓ {{delta}})
- Period to Date ({{periodLabel}}): avg {{rating}}★ across {{count}} prior weeks
- Prior Period ({{priorPeriodLabel}}): {{count}} total reviews at {{rating}}★

DAILY BREAKDOWN:
Monday {{date}}: {{positive}} positive, {{neutral}} neutral, {{negative}} negative
...

---

GENERATE THE REPORT USING EXACT METRICS. Format: # FEEDBACK REPORT, ## Venue,
## Week info, ### FEEDBACK BREAKDOWN (with exact numbers), ### REVIEW OBSERVATIONS
(4-5★, 3★, 1-2★), ### FEEDBACK TRENDS, ### FOCUS POINTS, ### NAME DROPS
```

## Why each section is there

**`COMPUTED METRICS (use these exact numbers)`** — the "use these exact numbers" phrasing is load-bearing. Without it, Claude will occasionally round, re-derive, or average in ways that drift from the JavaScript-computed values. This line makes the rule explicit.

**`RATING DISTRIBUTION` + `SOURCES`** — fed as lists, not as free-text, so the model doesn't paraphrase them. The final report echoes these verbatim.

**Deleted reviews broken out separately** — they're excluded from active metrics but included in the prompt so Claude can acknowledge "we removed X abusive reviews this week" when relevant. It also keeps the model from wondering why the numbers don't add up.

**Reviews grouped by promoter / neutral / detractor** — this is the main semantic grouping in the final report. Pre-grouping in the prompt means Claude writes each section independently and doesn't cross-contaminate themes between positive and negative feedback.

**`NAME MENTIONS` with the disclaimer** — the disclaimer is critical because the name-detection algorithm is intentionally lossy. Claude is explicitly told *not* to trust the names blindly and to flag them as needing human verification.

**`COMPARISONS FROM HISTORY`** — this section only appears if prior-week data exists in `metrics_history.json`. First-run reports don't get comparisons, which the model handles gracefully because the section is literally absent from the prompt rather than empty.

**Final format instruction** — strict section headers, in the exact order the GM expects. Every report the venue has ever received follows this skeleton, so the model's job is narrative only, never structure.

## Failure modes I've seen

- **Metric drift on first run.** Early versions didn't emphasize "use these exact numbers" strongly enough and Claude would occasionally re-average ratings from the raw reviews instead of trusting the pre-computed `weeklyAvg`. Fix: the "use these exact numbers" phrase + handing over the computed numbers *before* the raw reviews.
- **Paraphrasing quotes.** Claude used to slightly rewrite guest quotes "for clarity". Fix: explicit instruction in the final format block to quote verbatim, plus pre-formatting the reviews as bulleted verbatim lines.
- **Inventing focus points.** The "Focus Points" section is where the model can go off the rails if it doesn't have enough real signal. Fix: keep the prompt's review groupings dense with real text so the model always has something to point to, and accept that some weeks will have short focus sections.

## Model choice

Currently runs on `claude-sonnet-4-20250514`. Earlier versions used `gpt-4`. The switch to Claude was about consistency — the same prompt yielded more stable output formatting across runs on Claude than on GPT-4 at the time I ported the workflow. Worth re-evaluating when new model versions drop.
