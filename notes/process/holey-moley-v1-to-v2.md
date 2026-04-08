# Holey Moley Review Analytics — v1 Custom GPT → v2 Self-hosted n8n

The story of how a weekly admin task turned into a two-generation AI tool.

## The problem

At Holey Moley Austin (Funlab) I'm a shift manager and receptionist. Along with the usual floor duties, I was assigned the weekly guest-review reporting — read every review that came in through ReviewTrackers, summarize the themes, flag anything operationally relevant, and hand it to the GM and AGMs on Monday mornings.

The raw task: ~10–15 reviews a week across Google, Yelp, TripAdvisor. Not hard, not fast either. Reading them is fine. The annoying part is that every week you end up writing the same report structure — a rating summary, the recurring themes, the standout quotes, the staff callouts — from scratch. Copy-paste the header from last week, edit the dates, read everything again, re-type the narrative. Forty-five minutes of mechanical work to produce something that's 80% the same format every week.

That's the exact shape of a problem that AI solves cleanly.

## v1 — Custom GPT

The first version was the path of least resistance: build a Custom GPT on top of ChatGPT.

**What it did:** Accepted a ReviewTrackers CSV drop (export → upload), returned a themed weekly report in a consistent format — feedback breakdown, promoter/neutral/detractor sections, trends, focus points, name drops.

**How it worked:** A carefully-tuned system prompt with the report format baked in, a few-shot example of the desired output style, and instructions on how to handle deleted reviews, fiscal calendar math, and staff name detection.

**Who used it:** Me, at first. Then the GM of a sister venue in Denver asked if they could use something similar — I shared the GPT and they've been using it weekly ever since.

**Where it fell short for me personally:** I couldn't control the stack. Any OpenAI policy change, rate limit, or UX tweak affected how I worked. The data was going through OpenAI's hosted environment. And the report generation required me to manually export the CSV, open ChatGPT, upload, wait, copy, paste, save — a sequence of clicks that turned a 45-minute task into a 10-minute one, but still *my* clicks.

Also: the company is corporate and has guidelines on AI tools. The v1 GPT worked but it lived in a shared consumer account, which isn't a setup I wanted to scale.

## v2 — Self-hosted n8n

The rebuild lives on my own infrastructure. No shared accounts, no manual clicks, full pipeline control.

**The stack:**
- Self-hosted n8n (Docker) at `n8n.andre-espinoza.com`, exposed via a Cloudflare tunnel
- A watched Google Drive folder — I drop the ReviewTrackers CSV, the pipeline takes over
- A `metrics_history.json` file tracks running weekly metrics for week-over-week comparisons
- Claude API (via HTTP Request, not the native Anthropic n8n node — I wanted full control over the request body)
- Report gets filed automatically into a `FY24-25 / P01 / WK5` folder hierarchy on Drive
- Optional: a Telegram node at the end pings me with the Drive link and a one-line summary so I don't have to open Drive at all

**The key design choice:** *No AI in the math.* All the metrics — weekly average, rating distribution, source breakdown, deleted-review counts, year-to-date, period-to-date — are computed deterministically in a single Code node before Claude ever sees the data. The LLM only gets:

1. The exact pre-computed numbers (so it can't drift or hallucinate metrics)
2. The raw review text (so it can theme and quote)
3. A strict format instruction

This is the discipline that makes the pipeline trustworthy. If the GM ever asks "where did this number come from?" the answer is a deterministic JavaScript function, not a black-box model call.

**Fiscal calendar engine:** The venue runs a 52-week fiscal year (13 periods × 4 weeks) anchored to `2024-07-01`. The pipeline derives FY / period / week labels from the latest review date in the CSV, so back-filling old weeks lands in the right folder automatically.

**Name detection:** Automatically surfaces any capitalized 3+ letter word in a review that isn't in a stopword list — lossy by design. Better to surface three false positives than miss the one "Ask for Mariana, she's amazing!" that deserves a shoutout in the report.

## What changed after v2 shipped

The 10-minute workflow became *zero minutes in my hands* — the CSV lands, the report lands, Telegram pings me, I read and send it up the chain. I still push for reviews on the floor (making the report means I'm invested in the numbers), but the reporting itself is infrastructure now.

Over 15 months of owning this reporting loop, the venue's guest rating has moved from **4.06 to 4.89**. I wasn't the only variable — floor operations matter more than any report — but closing the feedback loop between what guests wrote and what the GM acted on is a meaningful part of that climb.

## What I'd change next

- **Smarter name deduplication** — the current stopword list needs manual maintenance as new staff join
- **Trend detection across periods** — right now the report compares to last week and period-to-date, but doesn't flag emerging multi-week patterns
- **Auto-drafted responses** — for now the GM still writes the replies on Google and Yelp. A v3 could draft contextual responses grounded in the venue's voice and the specific review

## The sanitized workflow

The full 22-node workflow is published as an open-source template: **[github.com/vnndre/weekly-review-bot](https://github.com/vnndre/weekly-review-bot)**. Credentials are stripped, venue-specific strings are placeholders, fiscal calendar constants are configurable. Clone, import into n8n, connect your own Google Drive and Anthropic credentials, drop a CSV, get a report.
