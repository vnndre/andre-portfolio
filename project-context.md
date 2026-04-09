# Project Context — Andre's Portfolio

> This file is the single source of truth for both Dev-Andre and Design-Andre.
> Both agents MUST read this file at the start of every session. When Andre
> points the agents at a new project, copy this file into the new project's
> root and fill it in for that project.

---

## Current project

- **Name:** Andre's Personal Portfolio
- **Location on Mac mini:** `~/projects/andre-portfolio`
- **Live URL:** https://andre-espinoza.com
- **Repo:** https://github.com/vnndre/andre-portfolio
- **Hosting:** Vercel (domain via Namecheap nameservers, auto-deploys on push to `main`)

## Tech stack

- **Framework:** None — static HTML, no build tools, no bundler
- **Language:** HTML, vanilla CSS, vanilla JS (no GSAP, no frameworks)
- **Styling:** All CSS inline in each `.html` file — no separate stylesheets
- **Content source:** Hand-authored HTML in the repo (no CMS)
- **Build command:** None
- **Dev command:** Open `index.html` directly, or `python3 -m http.server` from repo root
- **Deploy command / trigger:** `git push origin main` → Vercel auto-deploys

## About-me folder

- **Path:** `~/.claude/knowledge/about-me/` *(global knowledge base — not inside the repo)*
- **Contents:** bio (`Andre_Espinoza_Bio.docx`), résumé (`Resume.pdf`), LinkedIn/Instagram/Pinterest/Reddit exports, financial docs, WordPress portfolio content
- **Rule for both agents:** This folder is authoritative for anything about
  Andre personally. Never invent biographical facts. If something is missing
  or unclear, add a question below under "Questions for Andre".

## Brand & voice

*(Seeded from CLAUDE.md — Design-Andre can expand)*

- **Tone:** Deadpan, direct, slightly absurdist. Personal, not corporate-creative.
- **Voice examples (phrases that sound like you):** "pondering", real interests surfaced in marquee (Techno, Kapital, Glass Beams, Boiler Room)
- **Phrases to avoid:** Corporate-creative speak — "leveraging synergies", "passionate about", generic AI-assistant tone
- **Color palette:**
  - Background / ink black: `#050403`
  - Cream: `#ede6d8`
  - Accent / acid green: `#c8ff00`
  - Ember: `#ff6030`
  - Adobe / warm gold: `#c4956a`
- **Type scale:** Syne (display), Crimson Pro (body), JetBrains Mono (code)
- **Key references / inspiration:** *(Andre: add Awwwards / Godly / Dribbble refs)*

## Design system

- **Figma file URL:** *(Andre: paste Figma file URL)*
- **Production pages (do not touch without explicit approval):** `index.html`, `cartlog.html`, `aventi.html`, `broken-spoke.html`, `holey-moley.html`, `topper.html`
- **Draft page name:** `Design-Andre drafts`
- **Tokens source of truth:** Code — design tokens live inline in each HTML file's `<style>` block. There is no Figma variable library yet. *(Andre: confirm whether Figma should become source of truth)*

## Review process

- **Dev work:** Dev-Andre opens PRs on feature branches. Andre reviews and
  merges. Nothing auto-merges.
- **Design work:** Design-Andre drops drafts in Figma and markdown in the
  repo. Andre reviews before anything ships.
- **Cadence:** On-demand. Andre triggers a session when he has work to hand off.

## Dev-Andre TODO

*(Add tasks here. Dev-Andre works top-to-bottom unless priorities are marked.)*

- [ ] Audit package.json for unused dependencies and open a PR removing them. Keep the PR small — one dep per commit if possible. *(Note: this repo has no package.json yet — if none exists, instead audit `index.html` for unused `<link>`/`<script>` tags and dead CSS selectors and open a small PR.)*
- [ ]
- [ ]

## Design-Andre TODO

*(Add tasks here. Design-Andre works top-to-bottom unless priorities are marked.)*

- [ ] Run a WCAG 2.1 AA audit of the current portfolio home page and save the report to `design-reviews/2026-04-09-home-a11y.md`.
- [ ]
- [ ]

## Questions for Andre

*(Agents append questions here when they hit ambiguity. Andre answers and
the agents pick up from there next session.)*

-

## Dev-Andre session log

*(Dev-Andre appends a short entry every session.)*

-

## Design-Andre session log

*(Design-Andre appends a short entry every session.)*

-
