# Portfolio Redesign Log

A living document tracking visual + structural changes to andre-espinoza.com. The goal isn't "finished portfolio" — the goal is a portfolio that evolves as my work and taste evolve. This log makes the evolution visible.

## 2026-04-06 → 2026-04-08 — The warm texture shift

**Before:** Cold tech aesthetic. Ink black `#0a0a0a` background, antique gold `#c9a84c` accent, acid green `#c8f135` highlight, Unbounded + Shippori Mincho + IBM Plex Mono. Too much "startup dark mode", not enough of me.

**After:** Warm textured craft aesthetic. Same ink-black base but shifted toward `#050403`, cream `#ede6d8`, acid green `#c8ff00`, ember `#ff6030`, adobe gold `#c4956a`. Typography changed to Syne (display), Crimson Pro (body), JetBrains Mono (code). Added a visible grain overlay and warm vignette. Every case study page ported to match.

**Why:** The old palette read as "generic dark mode portfolio". The new palette reads as something specific — Texas heritage warmth, hand-made feeling, not a template. Matches my Instagram aesthetic (hand-cut collages, warm tones) and my fashion taste (workwear, raw denim, ember and gold tones).

## 2026-04-08 — Repo goes public

Moved `~/andre-portfolio/` to `~/Projects/andre-portfolio/` and published to [github.com/vnndre/andre-portfolio](https://github.com/vnndre/andre-portfolio). Added a README documenting the design system and architecture. Set up `.gitignore` to keep `.vercel/`, `*.mp4`, and working-asset folders out of the public repo.

## 2026-04-08 (in progress) — Structural overhaul + visual redesign v3

Planning a two-phase overhaul:

**Phase 1 — Structural (current):**
- Extract shared styles into `styles/design-system.css` so the design system lives in one file
- Extract shared JS (text scramble, magnetic cursor, grain canvas) into `scripts/common.js`
- Add `notes/process/` — process docs for each major case study (this file + cartlog + holey-moley)
- Add `notes/prompts/` — actual AI prompts used to build the case studies, documented
- Add `assets/case-studies/` — printed PDF exports of each case study for download
- Add `assets/research/` — interview notes, affinity maps, screeners
- Add `assets/figma/figma-share-links.md` — public Figma URLs for interactive prototypes

**Phase 2 — Visual redesign v3 (next):**
- Goal: glass + flowing + interactive, without looking like an AI template
- Research phase: gather 4–6 reference sites that nail the feel
- Teardown phase: decompose the references, identify the techniques worth stealing
- Rebuild: index.html first, then port case studies
- Explicit anti-goals: no purple gradients, no generic dark-and-techy, no Inter/Roboto, no "built with v0" energy

## Design principles I'm building toward

1. **Hand-made > templated.** Every animation should feel like a decision, not a default.
2. **Warm > cold.** The site should feel like it was written by a person, not a marketing team.
3. **Slow reveals > instant reveals.** Content should unfurl as the visitor moves through it. Motion earns attention — it shouldn't shout for it.
4. **Fewer, better interactions.** One magnetic cursor is memorable. Five micro-animations per section is nausea.
5. **Copy carries the weight.** No amount of motion can rescue boring writing. The voice is the through-line.

## Open questions

- Should each case study have its own micro-theme (different accent color, different texture) or strictly share the system?
- Is the hand-cut collage hero still right after v3, or does it need a rethink for "glass + flowing"?
- Desktop-only custom cursor: keep, evolve, or drop entirely?
- How much of this is really about shipping a better portfolio vs. using the portfolio as a design playground?
